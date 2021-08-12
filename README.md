# AWS extension package for Nextflow (xpack-amzn)

## Introduction

The AWS extension package is a plugin provided by [Seqera Labs](https://www.seqera.io/) that allows the support for [FSx for Lustre](https://aws.amazon.com/fsx/lustre/) 
and AWS [EFS](https://aws.amazon.com/efs/) file system when deploying Nextflow pipelines 
along with [AWS Batch](https://aws.amazon.com/batch/) computing service.

The plugin requires a license key to be used. If you are interested, please contact us for an evaluation license at [sales@seqera.io](mailto:sales@seqera.io).

## Configuration

1. Define the variable `NFX_XPACK_LICENSE` in your environment, e.g. 

    ```
    export NXF_XPACK_LICENSE=<license string>
    ```

2. Add in your pipeline `nextflow.config` file the following 
snippet: 

    ```
    plugins {
      id 'xpack-amzn@1.1.0'
    }
    ``` 

The number after `@` character represents the plugin version. Make sure to use 
a version matching your Nextflow version according the compatibility table 
in the following section. 

3. Follow the [documentation](docs.md) for configure feature specific settings (optional).

## Compatibility table


| Nextflow version      | Xpack version   |
|---                    |---              |
| 21.06.0-edge          | 1.1.0           |
| 21.01.1-edge, 21.04.x | 1.0.1           |


## License  

Copyright 2021, Seqera Labs, S.L. All Rights Reserved.