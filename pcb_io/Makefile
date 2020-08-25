#!/usr/bin/make

.PHONY: erc drc sch_fab pcb_fab erc_and_fab drc_and_fab

DEBUG=

all: erc_and_fab drc_and_fab

erc:
	kibot $(DEBUG) -d Fabrication -s run_drc -i

drc:
	kibot $(DEBUG) -d Fabrication -s run_erc -i

sch_fab:
	kibot $(DEBUG) -d Fabrication -s run_erc,run_drc  print_sch interactive_bom bom_html bom_xlsx bom_csv

pcb_fab:
	kibot $(DEBUG) -d Fabrication -s all print_front print_bottom gerbers excellon_drill gerber_drills position

erc_and_fab:
	kibot $(DEBUG) -d Fabrication -s run_drc  print_sch interactive_bom bom_html bom_xlsx bom_csv

drc_and_fab:
	kibot $(DEBUG) -d Fabrication -s run_erc print_front print_bottom gerbers excellon_drill gerber_drills position


