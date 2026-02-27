cmake_minimum_required(VERSION 3.20)
project(Legacy)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(Legacy
        src/main.cpp
        src/app/application.cpp
        src/platform/win32_window.cpp
        src/chat/message.cpp
        src/chat/layout_engine.cpp
        src/crypto/encryption.cpp
        src/storage/database.cpp
        src/network/client.cpp
        src/network/serializer.cpp
        src/media/gif_player.cpp
        src/media/image_cache.cpp
        src/graphics/renderer.cpp
        src/graphics/text_renderer.cpp
        src/graphics/image_loader.cpp
        src/ui/message_view.cpp
        src/ui/input_box.cpp
        src/ui/toolbar.cpp
        external/sqlite/sqlite3.c
)

set_source_files_properties(
        external/sqlite/sqlite3.c
        PROPERTIES LANGUAGE C
)

target_include_directories(Legacy PRIVATE
        external/asio/include
        external/sqlite
        external/libsodium/include
)

target_compile_definitions(Legacy PRIVATE
        UNICODE
        _UNICODE
        _WIN32_WINNT=0x0A00
)

target_link_directories(Legacy PRIVATE
        external/libsodium/lib
)

target_link_libraries(Legacy
        user32
        gdi32
        ws2_32
        d2d1
        dwrite
        windowscodecs
        sodium
)

target_link_options(Legacy PRIVATE -municode -mwindows)