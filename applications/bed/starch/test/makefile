TMP             = /tmp
USER           := $(shell whoami)
ORIGINAL_DATA  := ${TMP}/${USER}/starch_regression_test
THIS_DIR       := ${shell pwd}

all: input_data tests
	@echo "Congratulations, all Starch tests passed!"

input_data: random_bed_file 

tests: compression_and_extraction_tests concatenation_tests updating_tests metadata_integrity_tests

#
# setup of original (random) BED data
#

ORIGINAL_DIR    = ${THIS_DIR}/original_data
RANDOM_BED      = ${ORIGINAL_DATA}/data/random.bed

random_bed_file:
	@if [ -f ${RANDOM_BED} ]; then make -C ${ORIGINAL_DIR} -f makefile clean; fi;
	@make -C ${ORIGINAL_DIR} -f makefile random.bed

#
# compression and extraction
#

COMPEXT_DIR = ${THIS_DIR}/compression_and_extraction
COMPEXTRES_DIR = ${TMP}/${USER}/starch_regression_test/results/compression_and_extraction

compression_and_extraction_tests: random_bed_file
	@if [ -d ${COMPEXTRES_DIR} ]; then make -C ${COMPEXT_DIR} -f makefile clean; fi;
	@make -C ${COMPEXT_DIR} -f makefile all

#
# concatenation
#

CONCAT_DIR = ${THIS_DIR}/concatenation
CONCATRES_DIR = ${TMP}/${USER}/starch_regression_test/results/concatenation

concatenation_tests: random_bed_file compression_and_extraction_tests
	@if [ -d ${CONCATRES_DIR} ]; then make -C ${CONCAT_DIR} -f makefile clean; fi;
	@make -C ${CONCAT_DIR} -f makefile all

#
# updating
#

UPDATING_DIR = ${THIS_DIR}/updating
UPDATINGRES_DIR = ${TMP}/${USER}/starch_regression_test/results/updating

updating_tests: random_bed_file compression_and_extraction_tests
	@if [ -d ${UPDATINGRES_DIR} ]; then make -C ${UPDATING_DIR} -f makefile clean; fi;
	@make -C ${UPDATING_DIR} -f makefile all

#
# metadata integrity
#

MD_INTEG_DIR = ${THIS_DIR}/metadata_integrity
MD_INTEG_RES_DIR = ${TMP}/${USER}/starch_regression_test/results/metadata_integrity

metadata_integrity_tests: random_bed_file compression_and_extraction_tests
	@if [ -d ${MD_INTEG_RES_DIR} ]; then make -C ${MD_INTEG_DIR} -f makefile clean; fi;
	@make -C ${MD_INTEG_DIR} -f makefile all

#
# clean-up
#

clean:
	@echo "[STARCH] cleaning up files..."
	@make -C ${ORIGINAL_DIR} -f makefile clean
	@make -C ${COMPEXT_DIR} -f makefile clean
	@make -C ${CONCAT_DIR} -f makefile clean
	@make -C ${UPDATING_DIR} -f makefile clean
	@make -C ${MD_INTEG_DIR} -f makefile clean
	@rm -rf ${ORIGINAL_DATA}
