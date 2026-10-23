cmake_minimum_required(VERSION 3.16)
project(NetSentryDPI VERSION 2.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Header files location
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

find_package(Threads REQUIRED)

# Executable 1: packet_analyzer (Basic PCAP packet inspection and printing)
add_executable(packet_analyzer
    src/main.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
)

# Executable 2: dpi_engine (High-Performance Multi-threaded Deep Packet Inspection Engine)
add_executable(dpi_engine_bin
    src/dpi_mt.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
    src/sni_extractor.cpp
    src/types.cpp
)
target_link_libraries(dpi_engine_bin PRIVATE Threads::Threads)
set_target_properties(dpi_engine_bin PROPERTIES OUTPUT_NAME "dpi_engine")

# For macOS
if(APPLE)
    # Add any macOS-specific settings here
endif()
