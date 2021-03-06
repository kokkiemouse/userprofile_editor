cmake_minimum_required(VERSION 3.5)
add_subdirectory(qtaccountsservice)
project(userprofile_editor LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()
find_package(QT NAMES Qt6 Qt5 COMPONENTS Core Quick LinguistTools QuickControls2 Widgets REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core Quick LinguistTools QuickControls2 Widgets REQUIRED)
set(TS_FILES userprofile_editor_ja_JP.ts)
set(SOURCES
    main.cpp
    qml_signal_manager.cpp
    qml_signal_manager.h)

qt5_add_translation(QM_FILES ${TS_FILES})
qt5_create_translation(QM_FILES ${CMAKE_CURRENT_SOURCE_DIR} ${TS_FILES})
configure_file(translations.qrc ${CMAKE_CURRENT_BINARY_DIR} COPYONLY)
add_executable(userprofile_editor
      ${SOURCES}
      qml.qrc
      ${CMAKE_CURRENT_BINARY_DIR}/translations.qrc
      ${QM_FILES}
)
target_link_libraries(userprofile_editor PRIVATE QtAccountsService Qt${QT_VERSION_MAJOR}::Quick Qt${QT_VERSION_MAJOR}::QuickControls2 Qt${QT_VERSION_MAJOR}::Core)
qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
