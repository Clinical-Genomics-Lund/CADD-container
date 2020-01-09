Bootstrap:docker
From:nfcore/base

%labels
	MAINTAINER Viktor henmyr <viktor.henmyr@skane.se>
	DESCRIPTION Singularity container for CADD 1.5 GRCh38
	VERSION 0.0.1

%environment
#	export TMPDIR=/data/tmp # test might inherit host environment TMPDIR
%files
	/data/bnf/sw/cadd/1.5/CADD-scripts/ /opt/cadd/
	cadd_environment.yml /
	/trannel/cadd_1.5_hg38/data/annotations/GRCh38_v1.5/ /opt/cadd/data/annotations/GRCh38_v1.5/
%post
	/opt/conda/bin/conda env create -f /cadd_environment.yml
	/opt/conda/bin/conda clean -a
