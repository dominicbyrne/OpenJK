cmake_minimum_required(VERSION 2.8)
# For checks in subdirectories
set(InOpenJK TRUE)

#    Project name
project("OpenJK")

#    Customizable options
option(InstallDir "Where to install the binaries to" "${CMAKE_SOURCE_DIR}/install")
option(BuildMPEngine "Whether to create projects for the mp engine (jamp.exe)" ON)
option(BuildMPDed "Whether to create projects for the dedicated server (jampded.exe)" ON)
option(BuildMPGame "Whether to create projects for the mp serverside gamecode (jampgamex86.dll)" ON)
option(BuildMPCGame "Whether to create projects for the mp clientside gamecode (jampcgamex86.dll)" ON)
option(BuildMPUI "Whether to create projects for the mp ui code (jampuix86.dll)" ON)
if(WIN32)
	option(UseInternalOpenAL "Whether to use the included OpenAL instead of a locally installed one" ON)
endif(WIN32)

# Custom CMake Modules needed
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/CMakeModules" ${CMAKE_MODULE_PATH})

# Binary names
#set(SPEngine "openjksp")
set(SPEngine "jasp") #keep this unchanged until we've fixed the bug with the filename-workaround
set(SPGame "jagame")
set(SPCGame "jacgame")
#set(MPEngine "openjkmp")
set(MPEngine "jamp") #keep this unchanged until we've fixed the bug with the filename-workaround
set(MPGame "jampgame")
set(MPCGame "jampcgame")
set(MPBotlib "botlib")

# Paths
set(SPDir "${CMAKE_SOURCE_DIR}/code")
set(MPDir "${CMAKE_SOURCE_DIR}/codemp")
# shared code between mp and sp
set(LibsDir "${CMAKE_SOURCE_DIR}/libs")
set(Mp3Dir "${LibsDir}/mp3code")
set(PngDir "${LibsDir}/png")
set(EaxDir "${LibsDir}/eax")
set(OpenALDir "${LibsDir}/OpenAL")

set(Mp3Files
	"${Mp3Dir}/cdct.c"
	"${Mp3Dir}/config.h"
	"${Mp3Dir}/copyright.h"
	"${Mp3Dir}/csbt.c"
	"${Mp3Dir}/csbtb.c"
	"${Mp3Dir}/csbtl3.c"
	"${Mp3Dir}/cup.c"
	"${Mp3Dir}/cupini.c"
	"${Mp3Dir}/cupl1.c"
	"${Mp3Dir}/cupl3.c"
	"${Mp3Dir}/cwin.c"
	"${Mp3Dir}/cwinb.c"
	"${Mp3Dir}/cwinm.c"
	"${Mp3Dir}/htable.h"
	"${Mp3Dir}/hwin.c"
	"${Mp3Dir}/jdw.h"
	"${Mp3Dir}/l3.h"
	"${Mp3Dir}/l3dq.c"
	"${Mp3Dir}/l3init.c"
	"${Mp3Dir}/mdct.c"
	"${Mp3Dir}/mhead.c"
	"${Mp3Dir}/mhead.h"
	"${Mp3Dir}/mp3struct.h"
	"${Mp3Dir}/msis.c"
	"${Mp3Dir}/port.h"
	"${Mp3Dir}/small_header.h"
	"${Mp3Dir}/tableawd.h"
	"${Mp3Dir}/towave.c"
	"${Mp3Dir}/uph.c"
	"${Mp3Dir}/upsf.c"
	"${Mp3Dir}/wavep.c"
	)
set(EaxFiles
	"${EaxIncludeDir}/eax.h"
	"${EaxIncludeDir}/EaxMan.h"
	)

#    Add projects
#add_subdirectory(${SPDir})
add_subdirectory(${MPDir})