X86_64_building.md

Guile 1.8.8 builds fine for X86_64 on any linux distribution provided warnings are not considered as errors.

On the contrary, in Mingw-w64 building fails because on this platform the lengths of long and pointers differ, which causes errors in several files. I've made a quick-and-dirty patch to address these errors (I did not really take the time to think whether what I was doing was the completely appropriate thing to do). However, when applying this patch guile.exe builds, but it crashes immediatly when run. According to the links below there may be more things to fix (and it is not even done in Guile 2, AFAIU). Any help welcome.

Another way to remove compilation errors is to use configure the option --without-64-calls (and not the above patch), but the result is similar : guile.exe does not run.


maybe relevant information 
https://lists.gnu.org/archive/html/guile-commits/2010-11/msg00065.html
http://git.savannah.gnu.org/cgit/guile.git/commit/libguile?id=95643853d75f2dfe6209a2702ebb58248d606049
http://git.savannah.gnu.org/cgit/guile.git/commit/libguile?id=09b204d38756f0fa9ab4319874c8ce2838488dd0
http://git.savannah.gnu.org/cgit/guile.git/commit/libguile?id=eac7a5d03909291e62c671ead3d1c6a0ff84d4f0
