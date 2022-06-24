.. _devlog:

Contributing
============

Pull all your branches locally
Create a fork of the nekStab repo: https://github.com/ricardofrantz/nekStab
Add the new fork as a remote on your clone, e.g. git remote add personal https://github.com/your_user/nekStab 
Update branches to point at your personal repository: git branch —set-upstream-to=personal/master to track the master branch at your personal repository
You can then do git push/pull as before
If you want to be private then in the “Settings” on GitHub you change the visibility (it says you need to duplicate, you then need to push and pull appropriately, e.g. set “private” as the upstream repo, then push to public when you are finished with any publications for example)
Submit pull requests to the central nekStab repo from your fork
Of course if they have commit rights on the Central repo then they can just change their branches to point there, but it may be neater to avoid pushing directly to the central repository as we are seeking to have only the master branch publicly visible.


Changelog on Nek5000
====================

For reference here is a log with main changes from the nek5000_V19.tar.gz

.. topic:: /core/prepost.f

   change prepost.f line 1094 from "save nopen" to "common /RES_WANT/ nopen"

.. topic:: /tools/nekamg_setup/hypre/

   updated the repostory path to allow compilation