# DSi (TWL) SDMMC code

## Usage
* Call `TMIO_init()` once **after** irqInit() (libnds).
* Call `SDMMC_init(const u8 devNum)`.

If SDMMC_init() succeeded you can use all other SDMMC_...() functions. SDMMC_init() can be called again at any time to reinitialize the SD card/eMMC provided you call SDMMC_deinit() first.

DMA is supported for SDMMC_readSectors() and SDMMC_writeSectors() by passing a NULL pointer for buf and setting up a NDMA channel prior to calling these functions. Note that the TMIO driver does not support unaligned access for DMA and buffers not a multiple of 4 bytes (for CPU and DMA transfers). It's recommended to add a bounce buffer or cache to make sure buffers are 4 bytes aligned.