include_directories(include)
include_directories(../groupsock/include)
include_directories(../UsageEnvironment/include)
include_directories(../BasicUsageEnvironment/include)
ADD_DEFINITIONS(-D LOCALE_NOT_USED)

include_directories(${CMAKE_SOURCE_DIR}/include/openssl/)
# add ourself so  libcrypto.so    libssl.so
add_library(crypto
        SHARED
        IMPORTED)
set_target_properties(crypto
        PROPERTIES IMPORTED_LOCATION
        #E:/Projects/AndroidProjects/ASProject/Application2/app/src/main/jniLibs/libcrypto.so
        D:/jxdprojects/live555/app/src/main/cpp/liveMedia/jniLibs/${ANDROID_ABI}/libcrypto.so
        )

add_library(ssl
        SHARED
        IMPORTED)

#E:\Projects\AndroidProjects\ASProject\Application2\app\src\main\jniLibs\libssl.so
set_target_properties(ssl
        PROPERTIES IMPORTED_LOCATION
        #E:/Projects/AndroidProjects/ASProject/Application2/app/src/main/jniLibs/libssl.so
        D:/jxdprojects/live555/app/src/main/cpp/liveMedia/jniLibs/${ANDROID_ABI}/libssl.so
        )

file(GLOB liveMediaFiles
      *.cpp *.c)
list(APPEND LM_Dependence_SRC_LIST
            ../UsageEnvironment/HashTable.cpp
            ../UsageEnvironment/strDup.cpp
            ../groupsock/GroupsockHelper.cpp
            ../groupsock/Groupsock.cpp
            ../groupsock/inet.c
            ../groupsock/NetAddress.cpp
            ../groupsock/NetInterface.cpp
            ../groupsock/GroupEId.cpp
            ../BasicUsageEnvironment/BasicHashTable.cpp
        )
add_library(liveMedia SHARED ${liveMediaFiles} ${LM_Dependence_SRC_LIST})

target_link_libraries( # Specifies the target library.
        liveMedia

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib} crypto ssl)