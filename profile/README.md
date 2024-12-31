This is the cmake-remake project
================================

Somewhen end of summer 2024 there was a short conversation on #cmake IRC channel about starting a project to help all the little but important projects out there that lack the understanding of cmake or the manpower to deal with everything and have to focus on the code instead of build-system with that task. This idea now has grown and manfested in this project. The main purpose is to provide the projects with clean, functional cmake code that allows building on all supported plattforms.

Every project reworked here has at least the following feature:
* proper defined interfaces for consuming them as subprojects via add_subdirectory / git-submodule / fetchcontent
* proper exporting to get used as installed library on the system
* proper tests to ensure they can be used by other projects
* no additional external deps
* proper references if issues of the original project are close or pull-requests are incorporated/superseeded
