# Media Meta API

Filtering request  following `filters[]` params:
- `b2bSid` - StoneID of the stone on which media is searched. The match is not searched for the StoneID metadata field, but for the b2bSid field of the product in the Cutwise database (it may differ).
- `orientation` - orientation field value in DiBox / ViBox metadata. Case-sensitive.
- `projectId` - the value of the ProjectID field in the DiBox / ViBox metadata. Case-sensitive.
- `setupPreset` is the preset ID (like https://cutwise.com/api/v2/setuppresets). With custom media now there will be difficulties, perhaps in this case it is better to prefer the projectId.

Request example:
```
GET https://cutwise.com/api/v2/mediameta?access_token={TOKEN}&filters[orientation]=Crown&filters[setupPreset]=10&filters[b2bSid]=CUSHION0&limit=1
```
This query will return the metadata of the last downloaded ASET Black media for the stone CUSHION0 with `Orientation` attribute equals to `Crown`.
The total metadata list count (before limits) can be obtained in the X-Total-Count header from the server.

:grey_exclamation: Requests from users who do not have a ROLE_VENDOR benefit and / or who are not linked to any B2B will be banged with 403 status.
:grey_exclamation: Metadata is not issued in the original XML format, but in JSON with transformed base64 entities into strings.
:grey_exclamation: Issued metadata entities sorted in order of adding media to the database Cutwise (from new to old)
:grey_exclamation: All metadata gets into the output (prior to the beginning of media processing, as well as those media whose processing ended with an error)

API Response exmaple:
```
[
    {
        "id": 125654,
        "metaData": {
            "MovieMetaData": {
                "Z": "3.9000000131609779366734",
                "Gain": "1",
                "WB_B": "1.63857",
                "WB_R": "1.24243",
                "WB_G1": "0.915797",
                "WB_G2": "0.90683",
                "StoneID": "Cushion0",
                "XCenter": "-3.4",
                "YCenter": "1.0",
                "@version": "1",
                "Exposure": "7.5",
                "Hardware": "DiBox 2.0",
                "IsStereo": "1",
                "Software": "DiBox",
                "FrameRate": "25",
                "ProjectID": "24f89208-c01d-491e-98ee-345bf30cc58b",
                "XAmplitude": "5",
                "YAmplitude": "3",
                "FramesCount": "200",
                "Orientation": "Crown",
                "SetupPreset": "v1",
                "StereoAngle": "2.5",
                "LightingName": "Officelight black",
                "LDRImageIndex": "1",
                "RawPresetName": "Default",
                "HDRImagesCount": "2",
                "TrajectoryName": "Eight",
                "MetadataVersion": "2",
                "SoftwareVersion": "5.4.0.0",
                "StageHardwareType": "Gimbal",
                "IsOneWayTrajectory": "0",
                "ImagesToAverageCount": "3",
                "IsRear_1LightEnabled": "0",
                "IsRear_2LightEnabled": "0",
                "IsRing_1LightEnabled": "1",
                "IsRing_2LightEnabled": "1",
                "IsRing_3LightEnabled": "1",
                "IsRing_4LightEnabled": "1",
                "IsRing_6LightEnabled": "1",
                "IsRing_7LightEnabled": "1",
                "IsRing_8LightEnabled": "1",
                "IsRing_9LightEnabled": "1",
                "LightRing_1Brightness": "100",
                "LightRing_2Brightness": "100",
                "LightRing_3Brightness": "100",
                "LightRing_4Brightness": "100",
                "LightRing_6Brightness": "100",
                "LightRing_7Brightness": "10",
                "LightRing_8Brightness": "10",
                "LightRing_9Brightness": "100",
                "IsUV_365nmLightEnabled": "0",
                "IsUV_385nmLightEnabled": "0",
                "TonemappingAlgorithmVersion": "1.0"
            }
        }
    },
    {
        "id": 125642,
        "metaData": {
            "MovieMetaData": {
                "Z": "3.9000000131609779366734",
                "Gain": "1",
                "WB_B": "1.63857",
                "WB_R": "1.24243",
                "WB_G1": "0.915797",
                "WB_G2": "0.90683",
                "StoneID": "Cushion0",
                "XCenter": "-3.4",
                "YCenter": "1.0",
                "@version": "1",
                "Exposure": "30",
                "Hardware": "DiBox 2.0",
                "IsStereo": "1",
                "Software": "DiBox",
                "FrameRate": "25",
                "ProjectID": "24f89208-c01d-491e-98ee-345bf30cc58b",
                "XAmplitude": "5",
                "YAmplitude": "3",
                "FramesCount": "200",
                "Orientation": "Crown",
                "SetupPreset": "v1",
                "StereoAngle": "2.5",
                "LightingName": "Officelight black",
                "LDRImageIndex": "0",
                "RawPresetName": "Default",
                "HDRImagesCount": "2",
                "TrajectoryName": "Eight",
                "MetadataVersion": "2",
                "SoftwareVersion": "5.4.0.0",
                "StageHardwareType": "Gimbal",
                "IsOneWayTrajectory": "0",
                "ImagesToAverageCount": "3",
                "IsRear_1LightEnabled": "0",
                "IsRear_2LightEnabled": "0",
                "IsRing_1LightEnabled": "1",
                "IsRing_2LightEnabled": "1",
                "IsRing_3LightEnabled": "1",
                "IsRing_4LightEnabled": "1",
                "IsRing_6LightEnabled": "1",
                "IsRing_7LightEnabled": "1",
                "IsRing_8LightEnabled": "1",
                "IsRing_9LightEnabled": "1",
                "LightRing_1Brightness": "100",
                "LightRing_2Brightness": "100",
                "LightRing_3Brightness": "100",
                "LightRing_4Brightness": "100",
                "LightRing_6Brightness": "100",
                "LightRing_7Brightness": "10",
                "LightRing_8Brightness": "10",
                "LightRing_9Brightness": "100",
                "IsUV_365nmLightEnabled": "0",
                "IsUV_385nmLightEnabled": "0",
                "TonemappingAlgorithmVersion": "1.0"
            }
        }
    },
    {
        "id": 125598,
        "metaData": {
            "MovieMetaData": {
                "Z": "3.9000000131609779366734",
                "Gain": "1",
                "WB_B": "1.63857",
                "WB_R": "1.24243",
                "WB_G1": "0.915797",
                "WB_G2": "0.90683",
                "HDRMode": "EF",
                "StoneID": "Cushion0",
                "XCenter": "-3.4",
                "YCenter": "1.0",
                "@version": "1",
                "Exposure": "30",
                "Hardware": "DiBox 2.0",
                "IsStereo": "1",
                "Software": "DiBox",
                "FrameRate": "25",
                "ProjectID": "24f89208-c01d-491e-98ee-345bf30cc58b",
                "XAmplitude": "5",
                "YAmplitude": "3",
                "FramesCount": "200",
                "Orientation": "Crown",
                "SetupPreset": "v1",
                "StereoAngle": "2.5",
                "LightingName": "Officelight black",
                "RawPresetName": "Default",
                "HDRImagesCount": "2",
                "TrajectoryName": "Eight",
                "MetadataVersion": "2",
                "SoftwareVersion": "5.4.0.0",
                "StageHardwareType": "Gimbal",
                "IsOneWayTrajectory": "0",
                "ImagesToAverageCount": "3",
                "IsRear_1LightEnabled": "0",
                "IsRear_2LightEnabled": "0",
                "IsRing_1LightEnabled": "1",
                "IsRing_2LightEnabled": "1",
                "IsRing_3LightEnabled": "1",
                "IsRing_4LightEnabled": "1",
                "IsRing_6LightEnabled": "1",
                "IsRing_7LightEnabled": "1",
                "IsRing_8LightEnabled": "1",
                "IsRing_9LightEnabled": "1",
                "LightRing_1Brightness": "100",
                "LightRing_2Brightness": "100",
                "LightRing_3Brightness": "100",
                "LightRing_4Brightness": "100",
                "LightRing_6Brightness": "100",
                "LightRing_7Brightness": "10",
                "LightRing_8Brightness": "10",
                "LightRing_9Brightness": "100",
                "IsUV_365nmLightEnabled": "0",
                "IsUV_385nmLightEnabled": "0",
                "TonemappingAlgorithmVersion": "1.0"
            }
        }
    }
]
```
