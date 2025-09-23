### Rand al'Thor — Today at 9:13 PM
basically it is good practice to lock any mutexes used by a thread before joining the thread? (I mean lock from the thread calling the join) 
### Miuna — Today at 9:18 PM
No :thonk~2:
I can't begin to think of a situation in which that would do something good that join() doesn't, but i can think of many situations in which that'd cause a deadlock
### Rand al'Thor — Today at 9:19 PM
that's why I was wondering
ok
I'm a bit rusty on threads
### Mohsen Mirkarimi (aka Cthulhu) — Today at 9:22 PM
is std::jthread RAII and a thread is a resource?
### Darrell Wright(beached) — Today at 9:23 PM
auto lck = std::scoped_lock( mut );
th.join( );

Inside the thread 
auto lck = std::scoped_lock( mut );
// do stuff before finishing
one can dead lock by locking prior to join( )
interleave those in the worst way
### Eki — Today at 9:27 PM
std::jthread join()s on destruction, unlike std::thread
### Mohsen Mirkarimi (aka Cthulhu) — Today at 9:28 PM
so technically it acquires a thread resource?
### Eki — Today at 9:29 PM
If you mean "resource" in the RAII sense, then yeah I guess
Not necessarily how I would describe it
### Dada — Today at 9:36 PM
I don't think thread and jthread are different from that perspective.
If you let a thread die without calling join or detach, it will call terminate.
### __std::iso_exposer<λ> — Today at 9:43 PM
im a thread killa
(RAII edition)
### Rand al'Thor — Today at 9:51 PM
so if you don't need to terminate from the destructor (I mean you need to tell it to stop running yourself) then there is no reason to use it?
like for me I'm running a std::thread lambda within a DLL and joining it in DLL_PROCESS_DETACH of DllMain 
### Dada — Today at 9:55 PM
It wouldn't make a difference in this case but I would always use jthread if available, if only because that's what thread should've been to begin with.
i.e. it's a full replacement so you can forget the old one even exists.
### Darrell Wright(beached) — Today at 9:56 PM
right, jthread has a way to signal to the running thread that it should stop working.  plus diagnosing a waiting on join, deadlock, error vs a terminate is probably easier(more so in a debugger)
### Dada — Today at 9:58 PM
If your thread is a global variable in a dll, you can also make it a jthread and remove the manual join.
Or just leave it alone of course. 
### Rand al'Thor — Today at 9:58 PM
is that reliable?
### Darrell Wright(beached) — Today at 9:59 PM
is what reliable?
the dtor of the jthread object calls it 
### Dada — Today at 9:59 PM
I actually don't know, I'm assuming global variables are destroyed when the dll is unloaded.
### Darrell Wright(beached) — Today at 9:59 PM
oh that
I think FreeLibrary calls static destructors
not sure, nm
### Rand al'Thor — Today at 10:03 PM
I'm going to use DllMain DLL_PROCESS_DETACH because I need to set a std::atomic<bool> quitting global variable flag (that the thread checks) so the thread knows to quit the polling loop.. or am I overlooking something? 
### Dada — Today at 10:04 PM
Well that's another advantage of jthread: you can use the stop token feature instead of your quitting flag.
### Rand al'Thor — Today at 10:04 PM
ok I guess I better read up on what a stop token does
### Rand al'Thor — Today at 10:13 PM
yeah it does seem like a better design
### ben.craig — Today at 10:29 PM
I don't really like jthread.  Blocking operations in dtors can lead to very subtle code
And I really don't like stop token
### ❣ verodev ❣ — Today at 10:34 PM
What you don't like about stop token?
### ben.craig — Today at 10:36 PM
The store blocks while waiting on a user callback, and that can lead to deadlocks.  Calling unknown code while holding a lock is a big no-no
### ❣ verodev ❣ — Today at 10:38 PM
You can always assign your user callback to the std::stop_callback
### Christopher — Today at 10:38 PM
I don't think that mitigates the deadlock issue?
### ❣ verodev ❣ — Today at 10:38 PM
Well the stop callback will be called while the request to the stop source is made
### Rand al'Thor — Today at 10:39 PM
please explain why (about stop token - ok I guess i have more reading to do), I'm changing my code to use stop token.. however I'm uncomfortable relying on the destructor, so I'm still using DllMain to stop it - but using request_stop() now

the reason I'm uncomfortable is that I have some mutexes and such that are also global variables, and I don't want to have to keep everything in a specific declared order if I don't have to - I mean  I don't know what happens if they get destucted before the jthread 
### ❣ verodev ❣ — Today at 10:39 PM
So you could use that user callback to trampoline the control flow while the stop request is being processed
### Christopher — Today at 10:40 PM
That still doesn't get around being able to call unknown code while holding a lock.
### ben.craig — Today at 10:41 PM
The stop callback is the unknown code in question
### ❣ verodev ❣ — Today at 10:43 PM
Idk what you mean by unknown code exactly
You can control what is assigned to that callback
### ben.craig — Today at 10:45 PM
It's unknown to the stdlib.  There are other ways of formulating the guidance that may make more sense here.  "Don't call 'up' while holding a lock", where 'up' is from framework code into user code
### ❣ verodev ❣ — Today at 10:46 PM
I mean, with that logic we could also argue that what we assign an std::function instance with is also bad because it's unknown to the stdlib...
### ben.craig — Today at 10:47 PM
Std function doesn't hold a lock while invoking the callback
That's the big difference
### ❣ verodev ❣ — Today at 10:49 PM
I don't really see an issue with that as long as it's stated explicitly
### Christopher — Today at 10:51 PM
This is a sufficient reason to have it permanently excluded from safety-critical code methinks.
### ben.craig — Today at 10:51 PM
It makes it much harder to compose software.  Means you need to have very fine grained locking
### Rand al'Thor — Today at 10:52 PM
so good rule of thumb just don't use std::jthread if it's not already in the code?
### ben.craig — Today at 10:52 PM
To be fair, gracefully stopping a thread is hard.  You have a choice of  blocking on unregistering the callback (bad) or letting the callback fire after a bunch of stuff has already finished (tricky)
Jthread isn't terrible, but it's not my favorite.
If I have a locally scoped thread, then jthread is a reasonable thing to do.  The more picky I am about where the join needs to happen, the less likely I am to use jthread
### ❣ verodev ❣ — Today at 11:02 PM
Sure, jthread ain't meant to be a general purpose replace of thread, its aim is quite explicit and scoped: die when the stop_request is confirmed/processed and on the meantime you don't care about waiting for the completion of the jthread's dtor. It's for apps that don't care and just want their threads to join at some point after they run out of scope. If you on the other hand have to care much more about how your threads are managed what you need instead is a threadpool system that will allow you to have that kind of fine-grained control(explicit interrupts, reuse of threads when possible, ...), i think both approaches are fine and have some real-world usages
### Rand al'Thor — Today at 11:15 PM
good discussion