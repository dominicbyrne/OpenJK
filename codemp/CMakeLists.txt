cmake_minimum_required(VERSION 2.8)

# Make sure the user is not executing this script directly
if(NOT InOpenJK)
	message(FATAL_ERROR "Use the top-level cmake script!")
endif(NOT InOpenJK)

#    Add Game Project
# (TODO)

#    Add CGame Project
# (TODO)

#    Engine/Executable (jamp.exe)

find_package(OpenGL REQUIRED)