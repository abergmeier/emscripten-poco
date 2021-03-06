set(LIBNAME "PocoUtil")

set( BASE_SRCS
src/AbstractConfiguration.cpp
src/Application.cpp
src/ConfigurationMapper.cpp
src/ConfigurationView.cpp
src/FilesystemConfiguration.cpp
src/HelpFormatter.cpp
src/IniFileConfiguration.cpp
src/IntValidator.cpp
src/LayeredConfiguration.cpp
src/LoggingConfigurator.cpp
src/LoggingSubsystem.cpp
src/MapConfiguration.cpp
src/Option.cpp
src/OptionCallback.cpp
src/OptionException.cpp
src/OptionProcessor.cpp
src/OptionSet.cpp
src/PropertyFileConfiguration.cpp
src/RegExpValidator.cpp
src/ServerApplication.cpp
src/Subsystem.cpp
src/SystemConfiguration.cpp
src/Validator.cpp
src/XMLConfiguration.cpp
src/Timer.cpp
src/TimerTask.cpp
)

set( WIN_SRCS
src/WinRegistryConfiguration.cpp
src/WinRegistryKey.cpp
src/WinService.cpp
)

if(CMAKE_SYSTEM MATCHES "Windows")
 set(SRCS ${BASE_SRCS} ${WIN_SRCS})
 add_definitions(-DUtil_EXPORTS)
else (CMAKE_SYSTEM MATCHES "Windows")
 set(SRCS ${BASE_SRCS})
endif(CMAKE_SYSTEM MATCHES "Windows")

add_library( ${LIBNAME} ${LIB_MODE} ${SRCS} )
target_link_libraries( ${LIBNAME} PocoFoundation)

install(
    DIRECTORY include/Poco
    DESTINATION include
    PATTERN ".svn" EXCLUDE
    )
    
install(
    TARGETS ${LIBNAME}
    DESTINATION lib
    )


