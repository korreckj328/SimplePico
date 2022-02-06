cmake_minimum_required(VERSION 3.12)

# pull in sdk
include(pico_sdk_import.cmake)


project(hello_usb C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initialize the sdk
pico_sdk_init()

if (TARGET tinyusb_device)
	add_executable(hello_usb
					hello_usb.c
					)
	target_link_libraries(hello_usb pico_stdlib)

	pico_enable_stdio_usb(hello_usb 1)
	pico_enable_stdio_uart(hello_usb 0)

	pico_add_extra_outputs(hello_usb)
else()
	message(WARNING "not building")
	exit()
endif()

add_compile_options(-Wall
					-Wno-format
					-Wno-unused-function
					-Wno-maybe-unitialized
					)


