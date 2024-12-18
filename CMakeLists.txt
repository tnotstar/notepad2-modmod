cmake_minimum_required(VERSION 3.13)

project(notepad2-modmod
    VERSION 5.3.3
    DESCRIPTION "A free source code editing component"
    LANGUAGES C CXX
)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_EXE_LINKER_FLAGS "-static")
set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
set(BUILD_SHARED_LIBS OFF)

add_subdirectory(scintilla/)

set(NOTEPAD2_SOURCES
	src/Dialogs.c
	src/Dlapi.c
	src/Edit.c
	src/Helpers.c
	src/Notepad2.c
	src/Styles.c
	src/Print.cpp
)

set(NOTEPAD2_HEADERS
	src/Dialogs.h
	src/Dlapi.h
	src/Edit.h
	src/Helpers.h
	src/Notepad2.h
	src/SciCall.h
	src/Styles.h
	src/Resource.h
	src/Version.h
)

set(NOTEPAD2_DEFINITIONS
	UNICODE
	_UNICODE
)

add_executable(notepad2 ${NOTEPAD2_SOURCES} ${NOTEPAD2_HEADERS})

target_compile_definitions(notepad2 PRIVATE ${NOTEPAD2_DEFINITIONS})

target_include_directories(notepad2 PRIVATE src/ scintilla/include/ scintilla/lexlib/)

target_link_options(notepad2 PRIVATE -Wl,--subsystem,windows -mwindows -municode)
target_link_libraries(notepad2 PRIVATE -static scintilla kernel32 gdi32 comctl32 shell32 ole32 oleaut32 imm32 shlwapi msimg32)
