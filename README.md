# Knowledge base

Noting stuff down here for my reference, hopefully to prevent me from wasting time again investigating crap I don't want to spend time on, probaby will move it to some blog one day :)

## Speed up docker based development on Mac (and Windows)
As of 15th Aug 2018
and as of Docker Version 18.06.0-ce-mac70 (26399)

So it turns out that docker file I/O is horribly slow when developing via a VM of sorts on Mac and Windows but runs at native speed.

I have been trying to build a development pipeline which is smooth as possible end to end, you develop in 100% the same exact setup you will depoly the code in, for that it was a given that all development also happen within Docker.

Here are some solutions I tried:
- Native Docker for Mac gives 1800ms load time for a PHP 7.2 Symfony 4 hello world app with 0 logic.
- I tried VMWare with Ubuntu 18.04, basically run Docker natively in VM and ;oad up the code in it as a shared folder and share the VM connection back to the host using, load time went down to 200ms, its a nice solution if you want to keep the host OS also identical to deployment OS but VMWare aint free so...
- I tried VirtualBox, same setup, but vboxfs (Virtual Box File Sharing) from host to VM is a bit prolematic with regards to permissions and it's actually not that fast either.
- Then I ended up here -> http://docker-sync.io/ A bunch of smart guys have tried to solve this by syncing the code to the container instead of mounting it directly, basically lets the code run at native speed. Down to 80ms for the same page load.

In my testing I found docker-sync to be the best solution, although it did take some effort to read the docs and understand exactly how it works but I think it's worth it.

There were some issues getting `gem install docker` to install because my Brew, OpenSSL and Ruby were from the stoneage, trying to update them found more old dependencies, so that took a bit of time.
