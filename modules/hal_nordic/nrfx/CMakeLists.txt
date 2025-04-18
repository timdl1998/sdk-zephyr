# Copyright (c) 2021 Nordic Semiconductor ASA
# SPDX-License-Identifier: Apache-2.0

zephyr_library()

set(NRFX_DIR ${ZEPHYR_CURRENT_MODULE_DIR}/nrfx)
set(INC_DIR ${NRFX_DIR}/drivers/include)
set(SRC_DIR ${NRFX_DIR}/drivers/src)
set(MDK_DIR ${NRFX_DIR}/mdk)
set(HELPERS_DIR ${NRFX_DIR}/helpers)

zephyr_include_directories(${NRFX_DIR})
zephyr_include_directories(${INC_DIR})
zephyr_include_directories(${MDK_DIR})
zephyr_include_directories(.)

# Define MDK defines globally
zephyr_compile_definitions_ifdef(CONFIG_SOC_SERIES_NRF51X       NRF51)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF51822_QFAA       NRF51422_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF51822_QFAB       NRF51422_XXAB)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF51822_QFAC       NRF51422_XXAC)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52805            NRF52805_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52810            NRF52810_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52811            NRF52811_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52820            NRF52820_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52832            NRF52832_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52833            NRF52833_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_COMPATIBLE_NRF52833 NRF52833_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF52840            NRF52840_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF5340_CPUAPP      NRF5340_XXAA_APPLICATION)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF5340_CPUNET      NRF5340_XXAA_NETWORK)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF9120             NRF9120_XXAA)
zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF9160             NRF9160_XXAA)

zephyr_compile_definitions_ifdef(CONFIG_NRF_APPROTECT_LOCK
                                 ENABLE_APPROTECT)
zephyr_compile_definitions_ifdef(CONFIG_NRF_APPROTECT_USER_HANDLING
                                 ENABLE_APPROTECT_USER_HANDLING)
zephyr_compile_definitions_ifdef(CONFIG_NRF_SECURE_APPROTECT_LOCK
                                 ENABLE_SECURE_APPROTECT)
zephyr_compile_definitions_ifdef(CONFIG_NRF_SECURE_APPROTECT_USER_HANDLING
                                 ENABLE_SECURE_APPROTECT_USER_HANDLING)
zephyr_library_compile_definitions_ifdef(CONFIG_NRF_TRACE_PORT
                                 ENABLE_TRACE)

zephyr_compile_definitions_ifdef(CONFIG_SOC_NRF5340_CPUAPP
                                 NRF_SKIP_FICR_NS_COPY_TO_RAM)
zephyr_compile_definitions_ifdef(CONFIG_SOC_SERIES_NRF91X
                                 NRF_SKIP_FICR_NS_COPY_TO_RAM)

# Connect Kconfig compilation option for Non-Secure software with option required by MDK/nrfx
zephyr_compile_definitions_ifdef(CONFIG_ARM_NONSECURE_FIRMWARE NRF_TRUSTZONE_NONSECURE)
zephyr_compile_definitions_ifdef(CONFIG_LOG_BACKEND_SWO ENABLE_SWO)

zephyr_library_sources_ifdef(CONFIG_SOC_SERIES_NRF51X  ${MDK_DIR}/system_nrf51.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52805       ${MDK_DIR}/system_nrf52805.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52810       ${MDK_DIR}/system_nrf52810.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52811       ${MDK_DIR}/system_nrf52811.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52820       ${MDK_DIR}/system_nrf52820.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52832       ${MDK_DIR}/system_nrf52.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52833       ${MDK_DIR}/system_nrf52833.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF52840       ${MDK_DIR}/system_nrf52840.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF5340_CPUAPP ${MDK_DIR}/system_nrf5340_application.c)
zephyr_library_sources_ifdef(CONFIG_SOC_NRF5340_CPUNET ${MDK_DIR}/system_nrf5340_network.c)
zephyr_library_sources_ifdef(CONFIG_SOC_SERIES_NRF91X  ${MDK_DIR}/system_nrf91.c)

zephyr_library_sources(nrfx_glue.c)
zephyr_library_sources(${HELPERS_DIR}/nrfx_flag32_allocator.c)

zephyr_library_sources_ifdef(CONFIG_NRFX_PRS     ${SRC_DIR}/prs/nrfx_prs.c)

zephyr_library_sources_ifdef(CONFIG_NRFX_ADC     ${SRC_DIR}/nrfx_adc.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_CLOCK   ${SRC_DIR}/nrfx_clock.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_COMP    ${SRC_DIR}/nrfx_comp.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_DPPI    ${SRC_DIR}/nrfx_dppi.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_EGU     ${SRC_DIR}/nrfx_egu.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_GPIOTE  ${SRC_DIR}/nrfx_gpiote.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_I2S     ${SRC_DIR}/nrfx_i2s.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_IPC     ${SRC_DIR}/nrfx_ipc.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_LPCOMP  ${SRC_DIR}/nrfx_lpcomp.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_NFCT    ${SRC_DIR}/nrfx_nfct.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_NVMC    ${SRC_DIR}/nrfx_nvmc.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_PDM     ${SRC_DIR}/nrfx_pdm.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_POWER   ${SRC_DIR}/nrfx_power.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_PPI     ${SRC_DIR}/nrfx_ppi.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_PWM     ${SRC_DIR}/nrfx_pwm.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_QDEC    ${SRC_DIR}/nrfx_qdec.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_QSPI    ${SRC_DIR}/nrfx_qspi.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_RNG     ${SRC_DIR}/nrfx_rng.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_RTC     ${SRC_DIR}/nrfx_rtc.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_SAADC   ${SRC_DIR}/nrfx_saadc.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_SPI     ${SRC_DIR}/nrfx_spi.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_SPIM    ${SRC_DIR}/nrfx_spim.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_SPIS    ${SRC_DIR}/nrfx_spis.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_SYSTICK ${SRC_DIR}/nrfx_systick.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_TEMP    ${SRC_DIR}/nrfx_temp.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_TIMER   ${SRC_DIR}/nrfx_timer.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_TWI     ${SRC_DIR}/nrfx_twi.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_TWIM    ${SRC_DIR}/nrfx_twim.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_TWIS    ${SRC_DIR}/nrfx_twis.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_UART    ${SRC_DIR}/nrfx_uart.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_UARTE   ${SRC_DIR}/nrfx_uarte.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_USBD    ${SRC_DIR}/nrfx_usbd.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_USBREG  ${SRC_DIR}/nrfx_usbreg.c)
zephyr_library_sources_ifdef(CONFIG_NRFX_WDT     ${SRC_DIR}/nrfx_wdt.c)

if(CONFIG_NRFX_TWI OR CONFIG_NRFX_TWIM)
  zephyr_library_sources(${SRC_DIR}/nrfx_twi_twim.c)
endif()
