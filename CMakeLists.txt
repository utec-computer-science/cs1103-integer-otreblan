# Integer
# Copyright © 2020 otreblan
#
# integer is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# integer is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with integer.  If not, see <http://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 3.13.0)

# El nombre del proyecto
project(integer
	VERSION 0.0.0
	DESCRIPTION "Entero"
	HOMEPAGE_URL "https://github.com/utec-computer-science/cs1103-integer-otreblan"
	LANGUAGES "CXX"
)

# Sín esto el target_sources() no resuelve path's relativos.
cmake_policy(SET CMP0076 NEW)

# El programa en sí
add_library(${PROJECT_NAME} SHARED)

# Módulos de cmake
include(GNUInstallDirs)

# Version for the library symlinks
set_target_properties(${PROJECT_NAME}
	PROPERTIES
		VERSION ${PROJECT_VERSION}
		SOVERSION ${PROJECT_VERSION_MAJOR}
		CXX_STANDARD 17
)

# Source files
add_subdirectory(src)

# Headers
add_subdirectory(include)

# pkg-config
configure_file(${PROJECT_NAME}.pc.in
	${CMAKE_BINARY_DIR}/${PROJECT_NAME}.pc
	@ONLY
)
install(FILES
	${CMAKE_BINARY_DIR}/${PROJECT_NAME}.pc
	DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig
)

# Flags para el compilador
if(NOT DEFINED ENV{CXXFLAGS})
	set(CMAKE_CXX_FLAGS "-Wall -g")
endif()


# Definiciones para la instalación
install(TARGETS ${PROJECT_NAME}
	LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
