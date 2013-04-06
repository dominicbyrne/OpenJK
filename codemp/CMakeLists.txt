cmake_minimum_required(VERSION 2.8)

# Make sure the user is not executing this script directly
if(NOT InOpenJK)
	message(FATAL_ERROR "Use the top-level cmake script!")
endif(NOT InOpenJK)

#    Add Game Project
if(BuildMPGame)
	# (TODO)
endif(BuildMPGame)

#    Add CGame Project
if(BuildMPCGame)
	# (TODO)
endif(BuildMPCGame)

#    Add UI Project
if(BuildMPUI)
	# (TODO)
endif(BuildMPUI)


#        Common things between Engine and Dedicated Server
if(BuildMPEngine OR BuildMPDed)

	#    Botlib
	set(MPBotlibHeaderFiles
		"botlib/aasfile.h"
		"game/be_aas.h"
		"botlib/be_aas_bsp.h"
		"botlib/be_aas_cluster.h"
		"botlib/be_aas_debug.h"
		"botlib/be_aas_def.h"
		"botlib/be_aas_entity.h"
		"botlib/be_aas_file.h"
		"botlib/be_aas_funcs.h"
		"botlib/be_aas_main.h"
		"botlib/be_aas_move.h"
		"botlib/be_aas_optimize.h"
		"botlib/be_aas_reach.h"
		"botlib/be_aas_route.h"
		"botlib/be_aas_routealt.h"
		"botlib/be_aas_sample.h"
		"game/be_ai_char.h"
		"game/be_ai_chat.h"
		"game/be_ai_gen.h"
		"game/be_ai_goal.h"
		"game/be_ai_move.h"
		"game/be_ai_weap.h"
		"botlib/be_ai_weight.h"
		"game/be_ea.h"
		"botlib/be_interface.h"
		"game/botlib.h"
		"qcommon/cm_public.h"
		"qcommon/disablewarnings.h"
		"botlib/l_crc.h"
		"botlib/l_libvar.h"
		"botlib/l_log.h"
		"botlib/l_memory.h"
		"botlib/l_precomp.h"
		"botlib/l_script.h"
		"botlib/l_struct.h"
		"botlib/l_utils.h"
		"game/q_shared.h"
		"qcommon/qcommon.h"
		"qcommon/qfiles.h"
		"server/server.h"
		"game/surfaceflags.h"
		"qcommon/tags.h"
		)
	source_group("Header Files" "${MPBotlibHeaderFiles}")
	set(MPBotlibSourceFiles
		"botlib/be_aas_bspq3.cpp"
		"botlib/be_aas_cluster.cpp"
		"botlib/be_aas_debug.cpp"
		"botlib/be_aas_entity.cpp"
		"botlib/be_aas_file.cpp"
		"botlib/be_aas_main.cpp"
		"botlib/be_aas_move.cpp"
		"botlib/be_aas_optimize.cpp"
		"botlib/be_aas_reach.cpp"
		"botlib/be_aas_route.cpp"
		"botlib/be_aas_routealt.cpp"
		"botlib/be_aas_sample.cpp"
		"botlib/be_ai_char.cpp"
		"botlib/be_ai_chat.cpp"
		"botlib/be_ai_gen.cpp"
		"botlib/be_ai_goal.cpp"
		"botlib/be_ai_move.cpp"
		"botlib/be_ai_weap.cpp"
		"botlib/be_ai_weight.cpp"
		"botlib/be_ea.cpp"
		"botlib/be_interface.cpp"
		"botlib/l_crc.cpp"
		"botlib/l_libvar.cpp"
		"botlib/l_log.cpp"
		"botlib/l_memory.cpp"
		"botlib/l_precomp.cpp"
		"botlib/l_script.cpp"
		"botlib/l_struct.cpp"
		)
	source_group("Source Files" "${MPBotlibSourceFiles}")
	
	add_library("${MPBotlib}" STATIC "${MPBotlibHeaderFiles}" "${MPBotlibSourceFiles}")
	
	#    Common files/libraries/defines of both Engine and Dedicated Server
	
	# libraries: Botlib (more added later)
	set(MPEngineAndDedLibraries "${MPBotlib}")

	# libjpeg
	find_package(JPEG REQUIRED)
	set(MPEngineAndDedIncludeDirectories "${MPEngineAndDedIncludeDirectories}" "${JPEG_INCLUDE_DIR}")
	set(MPEngineAndDedLibraries "${MPEngineAndDedLibraries}" "${JPEG_LIBRARIES}")

	# zlib
	find_package(ZLIB REQUIRED)
	set(MPEngineAndDedIncludeDirectories "${MPEngineAndDedIncludeDirectories}" "${ZLIB_INCLUDE_DIRS}")
	set(MPEngineAndDedLibraries "${MPEngineAndDedLibraries}" "${ZLIB_LIBRARIES}")
	
	# PNG support
	set(MPEngineAndDedPNGFiles
		"${MPDir}/game/anims.h"
		"${MPDir}/game/bg_weapons.h"
		"${MPDir}/game/botlib.h"
		"${MPDir}/qcommon/disablewarnings.h"
		"${MPDir}/qcommon/platform.h"
		"${MPDir}/ui_public.h"
		)
	
	# Headers
	set(MPEngineAndDedHeaderFiles
		"${MPDir}/game/anims.h"
		"${MPDir}/game/bg_weapons.h"
		"${MPDir}/game/botlib.h"
		"${MPDir}/qcommon/disablewarnings.h"
		"${MPDir}/qcommon/platform.h"
		"${MPDir}/ui_public.h"
		)
	if(WIN32)
		set(MPEngineAndDedHeaderFiles "${MPEngineAndDedHeaderFiles}"
			"${MPDir}/win32/resource.h"
			)
	endif(WIN32)
	
	set(MPEngineAndDedCommonFiles
		"${MPDir}/qcommon/chash.h"
		"${MPDir}/qcommon/GenericParser2.cpp"
		"${MPDir}/qcommon/cm_landscape.h"
		"${MPDir}/qcommon/md4.cpp"
		"${MPDir}/qcommon/tags.h"
		"${MPDir}/qcommon/cm_randomterrain.h"
		"${MPDir}/qcommon/cm_draw.cpp"
		"${MPDir}/qcommon/cm_draw.h"
		"${MPDir}/qcommon/z_memman_pc.cpp"
		"${MPDir}/qcommon/cmd_common.cpp"
		"${MPDir}/qcommon/cm_randomterrain.cpp"
		"${MPDir}/qcommon/MiniHeap.h"
		"${MPDir}/qcommon/cm_public.h"
		"${MPDir}/qcommon/cm_polylib.h"
		"${MPDir}/qcommon/stringed_interface.cpp"
		"${MPDir}/qcommon/common.cpp"
		"${MPDir}/qcommon/stringed_ingame.cpp"
		"${MPDir}/qcommon/msg.cpp"
		"${MPDir}/qcommon/q_shared.cpp"
		"${MPDir}/qcommon/timing.h"
		"${MPDir}/qcommon/cm_trace.cpp"
		"${MPDir}/qcommon/files_common.cpp"
		"${MPDir}/qcommon/cm_polylib.cpp"
		"${MPDir}/qcommon/unzip.cpp"
		"${MPDir}/qcommon/vm_local.h"
		"${MPDir}/qcommon/cm_patch.h"
		"${MPDir}/qcommon/q_math.cpp"
		"${MPDir}/qcommon/qcommon.h"
		"${MPDir}/qcommon/vm_x86.cpp"
		"${MPDir}/qcommon/cm_local.h"
		"${MPDir}/qcommon/cvar.cpp"
		"${MPDir}/qcommon/GenericParser2.h"
		"${MPDir}/qcommon/RoffSystem.h"
		"${MPDir}/qcommon/net_chan.cpp"
		"${MPDir}/qcommon/cm_test.cpp"
		"${MPDir}/qcommon/cm_shader.cpp"
		"${MPDir}/qcommon/huffman.cpp"
		"${MPDir}/qcommon/cmd_pc.cpp"
		"${MPDir}/qcommon/files_pc.cpp"
		"${MPDir}/qcommon/vm_interpreted.cpp"
		"${MPDir}/qcommon/sstring.h"
		"${MPDir}/qcommon/game_version.h"
		"${MPDir}/qcommon/cm_terrain.cpp"
		"${MPDir}/qcommon/cm_patch.cpp"
		"${MPDir}/qcommon/unzip.h"
		"${MPDir}/qcommon/stringed_interface.h"
		"${MPDir}/qcommon/RoffSystem.cpp"
		"${MPDir}/qcommon/qfiles.h"
		"${MPDir}/qcommon/stringed_ingame.h"
		"${MPDir}/qcommon/vm.cpp"
		"${MPDir}/qcommon/cm_load.cpp"
		"${MPDir}/qcommon/cm_terrainmap.h"
		)
endif(BuildMPEngine OR BuildMPDed)

#        Engine/Executable (jamp.exe)

if(BuildMPEngine)
	#    Dependencies

	# OpenGL
	find_package(OpenGL REQUIRED)
	set(MPEngineIncludeDirectories "${MPEngineIncludeDirectories}" "${OPENGL_INCLUDE_DIR}")
	set(MPEngineLibraries "${MPEngineLibraries}" "${OPENGL_LIBRARIES}")

	# OpenAL (is optionally included for Windows)
	if(UseInternalOpenAL)
		set(MPEngineIncludeDirectories "${MPEngineIncludeDirectories}" "${OpenALDir}")
		# There's a libs/OpenAL32.lib
		find_library(OpenALLibrary NAMES OpenAL32 PATHS libs)
		set(MPEngineLibraries "${MPEngineLibraries}" "${OpenALLibrary}")
	else(UseInternalOpenAL)
		find_package(OpenAL REQUIRED)
		set(MPEngineIncludeDirectories "${MPEngineIncludeDirectories}" "${OPENAL_INCLUDE_DIR}")
		set(MPEngineLibraries "${MPEngineLibraries}" "${OPENAL_LIBRARY}")
	endif(UseInternalOpenAL)

	# EAX is Windows-Only (right?)
	if(WIN32)
		set(MPEngineIncludeDirectories "${MPEngineIncludeDirectories}" "${EaxDir}")
		set(MPEngineFiles "${MPEngineFiles}" "${EaxFiles}")
		source_group("EAX", "${EaxFiles}")
	endif(WIN32)

	#    Source Files
	
	# Common files
	set(MPEngineCommonFiles
		"${MPEngineAndDedCommonFiles}"
		"${MPDir}/cgame/cg_public.h"
		"${MPDir}/game/bg_public.h"
		"${MPDir}/renderer/qgl.h"
		"${MPDir}/qcommon/exe_headers.cpp"
		"${MPDir}/client/keys.h"
		"${MPDir}/game/surfaceflags.h"
		"${MPDir}/ui/keycodes.h"
		"${MPDir}/qcommon/CNetProfile.cpp"
		"${MPDir}/game/g_public.h"
		
		"${MPDir}/game/q_math.c"
		"${MPDir}/game/q_shared.h"
		"${MPDir}/qcommon/cm_terrainmap.cpp"
		"${MPDir}/qcommon/hstring.cpp"
		"${MPDir}/qcommon/hstring.h"
		"${MPDir}/qcommon/files.h"
		"${MPDir}/qcommon/INetProfile.h"
		"${MPDir}/qcommon/exe_headers.h"
		)
	source_group("Common" "${MPEngineCommonFiles}")

	# MP3 support
	set(MPEngineMP3Files "${MPEngineFiles}" "${Mp3Files}")
	source_group("MP3" "${Mp3Files}")

	# todo: windows resources

	add_executable("${MPBinary}" "${MPEngineFiles}")

endif(BuildMPEngine)

#        Dedicated Server (Engine) (jampded.exe)

if(BuildMPDed)
endif(BuildMPDed)