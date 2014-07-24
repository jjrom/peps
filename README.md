PEPS
====

Performance measurements of pre-processing tasks for PEPS Sentinels products ingestion.

Hardware
========
Measurements are done on the following hardware
* Macbook Pro 15 " (2013)
* Intel QuadCore i7 2,0 GHz processor (6 Mo shared N3 cache)
* 8 Go RAM DDR3L 1 600 MHz

Sentinel 1
==========
Des exemples de produits simulés sont accessibles [ici](http://scihub.esa.int/)

**S1A_IW_SLC__1SSH_20120109T054406_20120109T054424_001889_000001_E7DE.zip**

Taille du produit compréssé : 1.4 Go

Decompression
-------------

        time unzip S1A_IW_SLC__1SSH_20120109T054406_20120109T054424_001889_000001_E7DE.zip
        # real	0m26.410s
        # user	0m24.357s
        # sys	0m1.583s

Taille du produit décompréssé : 2.2 Go

Description
-----------
Le produit contient **3** images **TIFF** d'une taille de **665 Mo à 792 Mo**

        ls -hSl S1A_IW_SLC__1SSH_20120109T054406_20120109T054424_001889_000001_E7DE.SAFE/measurement/
        
Métriques
---------
Image **s1a-iw2-slc-hh-20120109t054407-20120109t054423-001889-000001-002.tiff**

| Caractéristique  |  Valeur         
| :----------------|:---------
| Type             | Interferometric Wide Swath
| Taille           | 792 Mo
| Format           | GeoTIFF
| Nb lignes        | 24461
| Nb colonnes      | 8490
| Nb de bandes     | 1
| Codage           | 16 bits
| Projection       | EPSG:4326 + GCP

**Tuilage EPSG:3857**
        
        time gdal2tiles.py s1a-iw2-slc-hh-20120109t054407-20120109t054423-001889-000001-002.tiff
        # real	5m18.497s
        # user	5m4.124s
        # sys	0m10.395s
        
        du -hs s1a-iw2-slc-hh-20120109t054407-20120109t054423-001889-000001-002
        # 136 Mo

** Taille du tuilage ** ~ 18 % de la donnée image décompréssée

Sentinel 2
==========
Des exemples de produits simulés sont accessibles ici - ftp://208.49.187.169/S2_Test_Product/

**S2A_OPER_PRD_MSIL1C_PDMC_20130621T120000_R065_V20091211T165928_20091211T170025.SAFE.tar**

Taille du produit compréssé : 4.1 Go

Decompression
-------------
        
        time tar -xf S2A_OPER_PRD_MSIL1C_PDMC_20130621T120000_R065_V20091211T165928_20091211T170025.SAFE.tar
        # real	1m0.838s
        # user	0m0.351s
        # sys	0m38.130s    

Taille du produit décompréssé : 4.1 Go

Description
-----------

Le produit contient **234** fichiers **JP2** d'une taille de **47 Ko à 85 Mo** réparties sur **18 granules**

Chaque granule contient **13** fichiers **JP2** (1 par bande). Un granule = 1 image
    
        # 234 images JP2
        ls -hSl S2A_OPER_PRD_MSIL1C_PDMC_20130621T120000_R065_V20091211T165928_20091211T170025.SAFE/GRANULE/*/IMG_DATA/*.jp2 | wc
        
        # Réparties sur 18 granules
        ls S2A_OPER_PRD_MSIL1C_PDMC_20130621T120000_R065_V20091211T165928_20091211T170025.SAFE/GRANULE/
        
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SMH_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLE_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SND_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLF_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SNE_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLG_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SNF_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLH_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SNG_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SMD_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPD_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SME_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPE_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SMF_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPF_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SMG_N01.01
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPG_N01.01


        # Exemple de contenu d'un granule (13 images JP2)
        ls S2A_OPER_PRD_MSIL1C_PDMC_20130621T120000_R065_V20091211T165928_20091211T170025.SAFE/GRANULE/S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_N01.01/IMG_DATA/
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B01.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B08.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B02.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B09.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B03.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B10.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B04.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B11.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B05.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B12.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B06.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B8A.jp2
        S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SLD_B07.jp2

Métriques
---------
Image **S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPE**

| Caractéristique  |  Valeur         
| :----------------|:---------
| Type             | MSI (MultiSpectral Instrument)
| Taille           | 124 Mo (13 fichiers)
| Format           | JPEG2000
| Nb lignes        | 10980
| Nb colonnes      | 10980
| Nb de bandes     | 1 par fichier (13 fichiers)
| Codage           | 16 bits
| Projection       | EPSG:32614 (UTM Zone 14N)

**Construction GeoTIF**
Le GeoTIFF est construit à partir des bandes B4, B3 et B2

        time gdal_merge.py -separate -o tmp.tif -of GTiff S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPE_B04.jp2 S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPE_B03.jp2 S2A_OPER_MSI_L1C_TL_CGS1_20130621T120000_A000065_T14SPE_B02.jp2
        # real	0m37.781s
        # user	0m33.314s
        # sys	0m3.257s
        
**Tuilage EPSG:3857**
        
        time gdal2tiles.py tmp.tif
        # real	2m9.177s
        # user	2m4.300s
        # sys	0m4.412s
        
        du -hs tmp
        # 42 Mo

** Taille du tuilage ** ~ 34 % de la donnée image décompréssée
