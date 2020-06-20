include_directories(include)
include_directories(../BasicUsageEnvironment/include)
include_directories(../groupsock/include)
#link_directories(${PROJECT_SOURCE_DIR}/main/jniLibs) #添加动态连接库的路径
#
#target_link_libraries (app libcrypto.so)
#target_link_libraries (app libsso.so)

file(GLOB UsageEnvironmentFiles
    *.cpp)
list(APPEND UE_Dependence_SRC_LIST
            ../BasicUsageEnvironment/BasicHashTable.cpp
        )
add_library(UsageEnvironment SHARED ${UsageEnvironmentFiles} ${UE_Dependence_SRC_LIST})