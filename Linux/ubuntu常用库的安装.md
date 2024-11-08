### 1. 安装opencv的库
[安装opencv4.5.0 c++](https://blog.csdn.net/weixin_44796670/article/details/115900538)

### 2. 安装gdal的库
1） 安装库
```shell
sudo apt install g++
sudo apt install libgdal-dev
sudo apt install gdal-bin
```
2） 验证
命令行验证
gdalinfo --version

代码验证：
编译命令：g++ test.cpp -o test_gdal -I/usr/include/gdal -L/usr/lib -lgdal
test.cpp
```c++
#include "gdal_priv.h"
#include "cpl_conv.h" // for CPLMalloc()

int main() {
    // 注册所有驱动
    GDALAllRegister();

    // 打开栅格文件
    GDALDataset *poDataset = (GDALDataset *) GDALOpen("path/to/your/raster/file.tif", GA_ReadOnly);
    if (poDataset == nullptr) {
        printf("文件无法打开\n");
        return 1;
    }

    // 打印驱动信息
    printf("Driver: %s/%s\n",
           poDataset->GetDriver()->GetDescription(),
           poDataset->GetDriver()->GetMetadataItem(GDAL_DMD_LONGNAME));

    // 打印栅格尺寸
    printf("Size is %dx%dx%d\n",
           poDataset->GetRasterXSize(),
           poDataset->GetRasterYSize(),
           poDataset->GetRasterCount());

    // 打印投影信息
    if (poDataset->GetProjectionRef() != nullptr)
        printf("Projection is `%s`\n", poDataset->GetProjectionRef());

    // 打印仿射变换信息
    double adfGeoTransform[6];
    if (poDataset->GetGeoTransform(adfGeoTransform) == CE_None) {
        printf("Origin = (%.6f, %.6f)\n", adfGeoTransform[0], adfGeoTransform[3]);
        printf("Pixel Size = (%.6f, %.6f)\n", adfGeoTransform[1], adfGeoTransform[5]);
    }

    // 打印第一个波段的信息
    GDALRasterBand *poBand = poDataset->GetRasterBand(1);
    int nBlockXSize, nBlockYSize;
    poBand->GetBlockSize(&nBlockXSize, &nBlockYSize);
    printf("Block=%dx%d Type=%s, ColorInterp=%s\n",
           nBlockXSize, nBlockYSize,
           GDALGetDataTypeName(poBand->GetRasterDataType()),
           GDALGetColorInterpretationName(poBand->GetColorInterpretation()));

    int bGotMin, bGotMax;
    double adfMinMax[2];
    adfMinMax[0] = poBand->GetMinimum(&bGotMin);
    adfMinMax[1] = poBand->GetMaximum(&bGotMax);
    if (!(bGotMin && bGotMax))
        GDALComputeRasterMinMax((GDALRasterBandH) poBand, TRUE, adfMinMax);
    printf("Min=%.3f, Max=%.3f\n", adfMinMax[0], adfMinMax[1]);

    if (poBand->GetOverviewCount() > 0)
        printf("Band has %d overviews.\n", poBand->GetOverviewCount());

    if (poBand->GetColorTable() != nullptr)
        printf("Band has a color table with %d entries.\n", poBand->GetColorTable()->GetColorEntryCount()); 
    // 关闭数据集
    GDALClose(poDataset); 
    return 0;
}
```
结果：
Driver: GTiff/GeoTIFF
Size is 2465x2310x3
Projection is `PROJCS["WGS 84 / World Mercator",GEOGCS["WGS 84",DATUM["WGS_1984",SPHEROID["WGS 84",6378137,298.257223563,AUTHORITY["EPSG","7030"]],AUTHORITY["EPSG","6326"]],PRIMEM["Greenwich",0,AUTHORITY["EPSG","8901"]],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AUTHORITY["EPSG","4326"]],PROJECTION["Mercator_1SP"],PARAMETER["central_meridian",0],PARAMETER["scale_factor",1],PARAMETER["false_easting",0],PARAMETER["false_northing",0],UNIT["metre",1,AUTHORITY["EPSG","9001"]],AXIS["Easting",EAST],AXIS["Northing",NORTH],AUTHORITY["EPSG","3395"]]`
Origin = (12106532.917606, 4008786.976418)
Pixel Size = (0.298582, -0.298582)
Block=2465x1 Type=Byte, ColorInterp=Red
Min=2.000, Max=255.000
