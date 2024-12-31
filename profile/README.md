This is the cmake-remake project
================================

Somewhen end of summer 2024 there was a short conversation on #cmake IRC channel about starting a project to help all the little but important projects out there that lack the understanding of cmake or the manpower to deal with everything and have to focus on the code instead of build-system with that task. This idea now has grown and manfested in this project. The main purpose is to provide the projects with clean, functional cmake code that allows building on all supported plattforms.

Every project reworked here has at least the following feature:
* proper defined interfaces for consuming them as subprojects via add_subdirectory / git-submodule / fetchcontent
* proper exporting to get used as installed library on the system
* proper tests to ensure they can be used by other projects
* no additional external deps
* proper references if issues of the original project are close or pull-requests are incorporated/superseeded
* integration of CPack

How to participate
==================
You can ask for an invitation on discussions, or on irc.libera.chat in #cmake. It's also possible to just get an invitation to this project when contributing to the rework by PR, or when you've recognized as engaged contributor on a reworked project.
If there are projects already mentioned in the issue-tracker here, that need to be reworked, feel free to wave and start the task.
If you're not able to work actively here but want to suggest a candidate for a rework, this is what the issue-tracker of this project is meant for. In the best case you are the maintainer of this project, if not you should have contacted the maintainer and you know it's not wasted time to consider the task.

Basic Rules
===========
* Get in touch with the projects maintainer BEFORE you start. Noone needs a 13th fork that improves something that won't get merged and just rotts.
* This is not about bringing every project to the bleeding edge of cmake, choose a reasonable minimum version depending on the projects aim. By now cmake < 3.10 is considered deprecated by the version used in the actions-runners, so this is the bare minimum. It's totally OK the stay there if no newer functions are needed by the project. But if you use i.e. HOMPAGE_URL in project, to be set in CPack created installers, which was introduced in 3.12, then bump to 3.12 not 3.15.
* This is not about changing the habbits of a project. If the indent with tabs, you indent with tabs. If they use conventional commits, you use conventional commits.
* This is not about adding external tools. If a project uses meson/vcpkg/cpm or anything like that, adjust what's needed to let it work like before. If they don't use something like that before, don't add it, this project here is plainly about cmake - nothing more, nothing less
* Keep things readable. There are many examples out there that use a huge amount of vars around everywhere. It's not more work to write NAME_SOMETHING instead of ${VAR}_SOMTHING but it's a pita to search maybe 10 different files to find that VAR is set to PROJECT_NAME. Most of this vars don't ever change, so it makes thing easier to just write what belongs there.
* Keep any subprojects selfcontained. It's fine to have an option to build some thirdparty extension from within the main build, but it has to be possible to also build these things on it's own without even relying on the original sources are present in let's say ../../. For sure, if the extension uses internal stuff only available in sources, this all is not possible.
* All tests from the original project need to be replacted. Tests shoud be name PROJECT_test-name to make it easier to select them in a run of ctest.
* Create targets for shared and static libs as otherwise to get them both 2 configure, compile runs are needed for no reason. Also test both of them.
* All options are prefixed with the projects name (yes, build-testing also) to have a nice gouping in cmake-gui when chainbuilding. If there are established options already, provide a little function that set their value if given as default and issue a warning that this is a deprecated option.
* Test also usage of find_package and add_subdirectory to make sure everything works as expected when the project is consumed.
* When commiting, mark every fixed or superseeded issue or PR in the original project to help them keeping track. If there are old reports that didn't apply or are just wrong usage and not closed, mention them to keep the tracker clean.
* Provide informations about en-/disabled optional features in the export-set
* Provide meaningfull components in the export set.
* Be aware that the maintainer could reach out to you to fix bugs in the future or review PRs. There's a reason why this project here is needed. As in general here will be no Issuetracker because the original project is the place for everything like that.
* When building static libs, link them to other static libs if possible. If you can't make sure it's a static lib you have, maybe that lib should be reworked beforehand.

TODO
====
* Provide examples for:
  * function for deprecating options
  * function for tests on plattforms with no rpath, so tests can find their libs without messing with output-paths
* Provide Issue template
