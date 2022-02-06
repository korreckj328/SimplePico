cmake_minimum_required(VERSION 3.12)
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)
# pull in sdk
include(pico_sdk_import.cmake)

project(hello_pico C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initialize the sdk
pico_sdk_init()

if (TARGET tinyusb_device)
	add_executable(hello_pico
					main.cpp
					)
	target_link_libraries(hello_pico pico_stdlib)

	pico_enable_stdio_usb(hello_pico 1)
	pico_enable_stdio_uart(hello_pico 0)

	pico_add_extra_outputs(hello_pico)
else()
	message(WARNING "not building")
	exit()
endif()

add_compile_options(-Wall
					-Wno-format
					-Wno-unused-function
					-Wno-maybe-unitialized
					)


