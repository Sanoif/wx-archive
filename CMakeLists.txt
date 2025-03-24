cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("wx-archive")
set(wxWidgets_ROOT_DIR "${CMAKE_SOURCE_DIR}/libs/wxWidgets")

find_package(
    
    wxWidgets REQUIRED
    
    gl core base
)
include(${wxWidgets_USE_FILE})

add_executable (wx-archive WIN32 "wx-archive.cpp"  "zippanel.h" "ignoringtraverser.h")
target_link_libraries(${PROJECT_NAME} PRIVATE ${wxWidgets_LIBRARIES})

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET wx-archive PROPERTY CXX_STANDARD 20)
endif()