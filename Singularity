Bootstrap:docker
From:nfcore/base:1.13

%labels
	MAINTAINER Viktor henmyr <viktor.henmyr@skane.se>
	DESCRIPTION Singularity container for CADD 1.5 GRCh38
	VERSION 0.0.1

%environment
	PATH=/opt/conda/envs/cadd-env/bin:/opt/conda/bin/:$PATH
#	export TMPDIR=/data/tmp # test might inherit host environment TMPDIR
%files
	cadd_environment.yml /

%setup
	cd /
	touch .condarc

%post
	rm -rf /var/lib/apt/lists/*
	apt -y clean
	apt -y update
	apt -y install libz-dev build-essential gettext cmake libxml2-dev libcurl4-openssl-dev libssl-dev make libbz2-dev graphicsmagick-imagemagick-compat
	
	/opt/conda/bin/conda env create -f /cadd_environment.yml python=3
	export PATH=/opt/conda/envs/cadd-env/bin:/opt/conda/bin:$PATH
	/opt/conda/bin/activate cadd-env
	cd / && git clone https://github.com/kircherlab/CADD-scripts.git
	cd /CADD-scripts
	
	/opt/conda/envs/cadd-env/bin/snakemake test/input.tsv.gz --use-conda \
		--create-envs-only \
		--conda-prefix envs \
		--configfile config/config_GRCh38_v1.6.yml \
		--cores 10 \
		--snakefile Snakefile
	ln -sr /fs1/viktor/misc-scripts
	cd data/annotations
	ln -sr /fs1/resources/ref/hg38/annotation_dbs/CADD_v1.6/data/annotations/GRCh38_v1.6 GRCh38_v1.6
	#/opt/conda/bin/conda install -c conda-forge mamba
	#mamba create -c conda-forge -c bioconda -n snakemake snakemake
	#/opt/conda/bin/conda clean -a


	