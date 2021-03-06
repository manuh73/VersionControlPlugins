IF (WIN32)
	CM_CONFIGURE_MSVC_RUNTIME()
ENDIF (WIN32)

CM_TARGET_BEGIN(
	TestServer
	EXECUTABLE
	.
	TestServer
)	
	# Dependencies
	# -----------------------------------------------
	
	# Includes
	# -----------------------------------------------
	CM_TARGET_ADD_INCLUDES(../Common)
	
	# Defines
	# -----------------------------------------------
	
	# Sources
	# -----------------------------------------------
	CM_TARGET_ADD_SOURCES( 
		"Common"
        ../Common/Changes.cpp
        ../Common/Changes.h
        ../Common/Command.cpp
        ../Common/Command.h
        ../Common/CommandLine.cpp
        ../Common/CommandLine.h
        ../Common/Connection.cpp
        ../Common/Connection.h
        ../Common/Dispatch.h
        ../Common/FileSystem.cpp
        ../Common/FileSystem.h
        ../Common/Log.cpp
        ../Common/Log.h
        ../Common/Pipe.cpp
        ../Common/Pipe.h
        ../Common/POpen.cpp
        ../Common/POpen.h
        ../Common/Status.cpp
        ../Common/Status.h
        ../Common/Utility.cpp
        ../Common/Utility.h
        ../Common/VersionControlPlugin.cpp
        ../Common/VersionControlPlugin.h
        ../Common/VersionedAsset.cpp
        ../Common/VersionedAsset.h
	)
	
	CM_TARGET_ADD_SOURCES( 
		"Sources"
		./Source/ExternalProcess.h
		./Source/TestServer.cpp
	)
	
	IF (APPLE)
		CM_TARGET_ADD_SOURCES( 
			"Sources"
			./Source/ExternalProcess_Posix.cpp
		)
	ENDIF (APPLE)
	
	IF (WIN32)
		CM_TARGET_ADD_SOURCES( 
			"Sources"
			./Source/ExternalProcess_WIN.cpp
		)
	ENDIF (WIN32)
	
	IF (UNIX AND NOT APPLE)
		CM_TARGET_ADD_SOURCES( 
			"Sources"
			./Source/ExternalProcess_Posix.cpp
		)
	ENDIF (UNIX AND NOT APPLE)

	# Libraries
	# -----------------------------------------------
	IF (APPLE)
		CM_TARGET_ADD_LIBRARIES(
		)
	ENDIF (APPLE)
	
	IF (WIN32)
		CM_TARGET_ADD_LIBRARIES(
			shlwapi.lib
		)
	ENDIF (WIN32)
	
	IF (UNIX AND NOT APPLE)
		CM_TARGET_ADD_LIBRARIES(
		)
	ENDIF (UNIX AND NOT APPLE)
	
	# Link flags
	# -----------------------------------------------
	IF (APPLE)
		CM_TARGET_ADD_LINK_FLAGS ( "-arch i386 -g -framework Cocoa -lstdc++" )
	ENDIF (APPLE)
	
	IF (WIN32)
		CM_TARGET_ADD_LINK_FLAGS ( "" )
	ENDIF (WIN32)

	IF (UNIX AND NOT APPLE)
		CM_TARGET_ADD_LINK_FLAGS ( "-g -fpermissive -lrt -ldl -lstdc++" )
	ENDIF (UNIX AND NOT APPLE)
	
# End of target definition
# -----------------------------------------------
CM_TARGET_END()