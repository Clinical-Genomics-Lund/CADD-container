Bootstrap:docker
From:nfcore/base

%labels
	MAINTAINER Viktor henmyr <viktor.henmyr@skane.se>
	DESCRIPTION Singularity container for CADD 1.4
	VERSION 0.0.1

%environment
#	export TMPDIR=/data/tmp # test might inherit host environment TMPDIR
%files
	/data/bnf/sw/cadd/1.5/CADD-scripts/ /opt/cadd/
	cadd_environment.yml /
	add_missing_CADDs_1.4.sh /opt/
	/data/bnf/sw/cadd/1.4/CADD-scripts/data/annotations/GRCh37 /opt/cadd/data/annotations/GRCh37_v1.4/
%post
	/opt/conda/bin/conda env create -f /cadd_environment.yml
	/opt/conda/bin/conda clean -a
