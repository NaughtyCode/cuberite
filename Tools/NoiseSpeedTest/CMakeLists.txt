project (NoiseSpeedTest)

include(../../SetFlags.cmake)
set_flags()
set_lib_flags()
enable_profile()

# Set include paths to the used libraries:
include_directories(SYSTEM "../../lib")
include_directories("../../src")

set_exe_flags()

# Include the shared files:
set(SHARED_SRC
	../../src/Logger.cpp
	../../src/LoggerListeners.cpp
	../../src/OSSupport/CriticalSection.cpp
	../../src/OSSupport/File.cpp
	../../src/OSSupport/StackTrace.cpp
	../../src/Noise/Noise.cpp
	../../src/StringUtils.cpp
)
set(SHARED_HDR
	../../src/Noise/Noise.h
	../../src/Noise/OctavedNoise.h
	../../src/Noise/RidgedNoise.h
	../../src/OSSupport/CriticalSection.h
	../../src/OSSupport/File.h
	../../src/OSSupport/StackTrace.h
	../../src/StringUtils.h
)

if(WIN32)
	list (APPEND SHARED_SRC ../../src/StackWalker.cpp)
	list (APPEND SHARED_HDR ../../src/StackWalker.h)
endif()

source_group("Shared" FILES ${SHARED_SRC} ${SHARED_HDR})




# Include the main source files:
set(SOURCES
	NoiseSpeedTest.cpp
	Globals.cpp
)
set(HEADERS
	NoiseSpeedTest.h
	Globals.h
)

source_group("" FILES ${SOURCES} ${HEADERS})

add_executable(NoiseSpeedTest
	${SOURCES}
	${HEADERS}
	${SHARED_SRC}
	${SHARED_HDR}
)

set_target_properties(
	NoiseSpeedTest
	PROPERTIES FOLDER Tools
)
