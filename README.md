# rMATS (Docker)
Docker to run rMATS for splicing quantification and analysis

## Available software
- [rMATS](http://rnaseq-mats.sourceforge.net) 4.0.2 (run using `python ${rmats}/RNASeq-MATS.py`)
- [samtools](http://htslib.org) 1.9
- [STAR](https://github.com/alexdobin/STAR) 2.5.3a
- [python 2.7](https://python.org)

## Maintainer
Ittai Muller (i.muller@vumc.nl) adapted from Nuno Agostintho (github.com/nuno-agostinho)

## Building
`docker build . -t rdeboo/rmats:4.0.2-3`

## Testing
```
#download test data
mkdir data
wget -qO- https://datapacket.dl.sourceforge.net/project/rnaseq-mats/MATS/gtf.tgz | tar xvz -C data/
wget -qO- https://netcologne.dl.sourceforge.net/project/rnaseq-mats/MATS/testData.tgz | tar xvz -C data/

# run container
docker run -ti -v $(pwd)data:/data rdeboo/rmats:4.0.2-3 bash

# run these commands inside container
cd /data/testData

python /root/software/rmats/rMATS-turbo-Linux-UCS4/rmats.py \
--b1 /data/testData/b1.txt --b2 /data/testData/b2.txt \
--gtf /data/gtf/Homo_sapiens.Ensembl.GRCh37.75.gtf \
--od /data/output -t paired --readLength 101 --cstat 0.0001 --libType fr-unstranded
```

Note that the output is written in `/data` which is a directory on the host VM. Therefore the output is persisted after the docker container is exited.

