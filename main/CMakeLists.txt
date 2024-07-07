file(TO_CMAKE_PATH "$ENV{MRD_INCLUDE_PATH}" MRD_INCLUDE_PATH)
idf_component_register(
    SRCS "main.c"
    INCLUDE_DIRS ". "
    ${MRD_INCLUDE_PATH}
    
    # REQUIRES esp_https_server nvs_flash bt json driver console esp_http_client 
    # app_update bootloader bootloader_support 
    REQUIRES app_update esp_https_ota app_update esp_http_client console driver json bt nvs_flash esp_https_server 
    # esp_event nvs_flash bt esp_eth esp_http_client esp_http_server json 
    #     console app_update esp_https_ota mbedtls  bootloader_support
    # REQUIRES bootloader bootloader_support 
    )

add_prebuilt_library(myRemoteDevice "libmyRemoteDevice.a"
PRIV_REQUIRES spi_flash app_update log console espressif__led_strip)
target_link_libraries(${COMPONENT_LIB} PRIVATE myRemoteDevice)

