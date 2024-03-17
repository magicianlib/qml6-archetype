cmake_minimum_required(VERSION 3.16)

project(qml6-archetype VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.5 REQUIRED COMPONENTS Quick)

qt_standard_project_setup(REQUIRES 6.5)

# 源文件
set(SOURCES
  main.cpp
)

# 资源文件
qt_add_resources(RESOURCES
  images.qrc
  # 其他资源文件
)

# 大文件
# qt_add_big_resources(BIG_RESOURCES)

# 二进制资源文件
# qt_add_binary_resources(BINARY_RESOURCES)

qt_add_executable(qml6-archetype
    ${SOURCES}
    ${RESOURCES}
    # ${BIG_RESOURCES}
    # ${BINARY_RESOURCES}
)

set(QML_RESOURCES
 app/Window.qml

  app/Head.qml
  app/Body.qml
  app/Footer.qml

  app/body/Menu.qml
  app/body/Content.qml
)

qt_add_qml_module(qml6-archetype
    URI qml6-archetype
    VERSION 1.0
    QML_FILES ${QML_RESOURCES}
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(qml6-archetype PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.qml6-archetype
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(qml6-archetype
    PRIVATE Qt6::Quick
)

include(GNUInstallDirs)
install(TARGETS qml6-archetype
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
