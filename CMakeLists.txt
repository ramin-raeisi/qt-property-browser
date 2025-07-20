
find_package(Qt6 REQUIRED COMPONENTS Core Widgets)

add_library(QtPropertyBrowser SHARED)

target_sources(QtPropertyBrowser
  PRIVATE
    qtpropertybrowser_p.h
    qtpropertymanager_p.h
    qteditorfactory_p.h
    qtvariantproperty_p.h
    qttreepropertybrowser_p.h
    qtbuttonpropertybrowser_p.h
    qtgroupboxpropertybrowser_p.h
    qtpropertybrowserutils_p.h
    qtpropertybrowser.cpp
    qtpropertymanager.cpp
    qteditorfactory.cpp
    qtvariantproperty.cpp
    qttreepropertybrowser.cpp
    qtbuttonpropertybrowser.cpp
    qtgroupboxpropertybrowser.cpp
    qtpropertybrowserutils.cpp
)

include(GenerateExportHeader)
generate_export_header(QtPropertyBrowser
  BASE_NAME QTPROPERTYBROWSER
  EXPORT_MACRO_NAME QTPROPERTYBROWSER_API
  EXPORT_FILE_NAME ${CMAKE_CURRENT_BINARY_DIR}/QtPropertyBrowserExport.h
)

if(MSVC)
  target_compile_options(QtPropertyBrowser PUBLIC /FI${CMAKE_CURRENT_BINARY_DIR}/QtPropertyBrowserExport.h /W0)
elseif(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang|AppleClang")
  target_compile_options(QtPropertyBrowser PUBLIC -include ${CMAKE_CURRENT_BINARY_DIR}/QtPropertyBrowserExport.h -w)
endif()

target_include_directories(QtPropertyBrowser
  PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}
    $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>
)

set_target_properties(QtPropertyBrowser
  PROPERTIES 
    AUTOMOC ON
)

target_link_libraries(QtPropertyBrowser
  PRIVATE
    Qt6::Core
    Qt6::Widgets
)
