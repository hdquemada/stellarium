INCLUDE_DIRECTORIES(
     .
     gui
     ${CMAKE_BINARY_DIR}/plugins/Quasars/src
     ${CMAKE_BINARY_DIR}/plugins/Quasars/src/gui
)

LINK_DIRECTORIES(${CMAKE_BINARY_DIR}/src)

SET(Quasars_SRCS
     Quasars.hpp
     Quasars.cpp
     Quasar.hpp
     Quasar.cpp
     gui/QuasarsDialog.hpp
     gui/QuasarsDialog.cpp
)

SET(QuasarsDialog_UIS
     gui/quasarsDialog.ui
)

SET(Quasars_RES ../resources/Quasars.qrc)

IF (${QT_VERSION_MAJOR} EQUAL "5")
     QT5_WRAP_UI(QuasarsDialog_UIS_H ${QuasarsDialog_UIS})
     QT5_ADD_RESOURCES(Quasars_RES_CXX ${Quasars_RES})
ELSE()
     QT_WRAP_UI(QuasarsDialog_UIS_H ${QuasarsDialog_UIS})
     QT_ADD_RESOURCES(Quasars_RES_CXX ${Quasars_RES})
ENDIF()

ADD_LIBRARY(Quasars-static STATIC ${Quasars_SRCS} ${Quasars_RES_CXX} ${QuasarsDialog_UIS_H})
TARGET_LINK_LIBRARIES(Quasars-static Qt${QT_VERSION_MAJOR}::Core Qt${QT_VERSION_MAJOR}::Network Qt${QT_VERSION_MAJOR}::Widgets)
SET_TARGET_PROPERTIES(Quasars-static PROPERTIES OUTPUT_NAME "Quasars")
SET_TARGET_PROPERTIES(Quasars-static PROPERTIES COMPILE_FLAGS "-DQT_STATICPLUGIN")
ADD_DEPENDENCIES(AllStaticPlugins Quasars-static)

SET_TARGET_PROPERTIES(Quasars-static PROPERTIES FOLDER "plugins/Quasars")
