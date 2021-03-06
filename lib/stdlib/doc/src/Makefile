#
# %CopyrightBegin%
#
# Copyright Ericsson AB 1997-2011. All Rights Reserved.
#
# The contents of this file are subject to the Erlang Public License,
# Version 1.1, (the "License"); you may not use this file except in
# compliance with the License. You should have received a copy of the
# Erlang Public License along with this software. If not, it can be
# retrieved online at http://www.erlang.org/.
#
# Software distributed under the License is distributed on an "AS IS"
# basis, WITHOUT WARRANTY OF ANY KIND, either express or implied. See
# the License for the specific language governing rights and limitations
# under the License.
#
# %CopyrightEnd%
#
include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Application version
# ----------------------------------------------------
include ../../vsn.mk
VSN=$(STDLIB_VSN)
APPLICATION=stdlib

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/lib/$(APPLICATION)-$(VSN)

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------
XML_APPLICATION_FILES = ref_man.xml

XML_REF3_FILES = \
	array.xml \
	base64.xml \
	beam_lib.xml \
	binary.xml \
	c.xml \
	calendar.xml \
	dets.xml \
	dict.xml \
	digraph.xml \
	digraph_utils.xml \
	epp.xml \
	erl_eval.xml \
	erl_expand_records.xml \
	erl_id_trans.xml \
	erl_internal.xml \
	erl_lint.xml \
	erl_parse.xml \
	erl_pp.xml \
	erl_scan.xml \
	erl_tar.xml \
	ets.xml \
	file_sorter.xml \
	filelib.xml \
	filename.xml \
	gb_sets.xml \
	gb_trees.xml \
	gen_event.xml \
	gen_fsm.xml \
	gen_server.xml \
	io.xml \
	io_lib.xml \
	lib.xml \
	lists.xml \
	log_mf_h.xml \
	math.xml \
	ms_transform.xml \
	orddict.xml \
	ordsets.xml \
	pg.xml \
	pool.xml \
	proc_lib.xml \
	proplists.xml \
	qlc.xml \
	queue.xml \
	random.xml \
	re.xml \
	sets.xml \
	shell.xml \
	shell_default.xml \
	slave.xml \
	sofs.xml \
	string.xml \
	supervisor.xml \
	supervisor_bridge.xml \
	sys.xml \
	timer.xml \
	unicode.xml \
	win32reg.xml \
	zip.xml

XML_REF6_FILES = stdlib_app.xml

XML_PART_FILES = part.xml part_notes.xml part_notes_history.xml
XML_CHAPTER_FILES = io_protocol.xml unicode_usage.xml notes.xml notes_history.xml
GIF_FILES = ushell1.gif ushell2.gif ushell3.gif

BOOK_FILES = book.xml

XML_FILES = \
	$(BOOK_FILES) $(XML_CHAPTER_FILES) \
	$(XML_PART_FILES) $(XML_REF3_FILES) $(XML_REF6_FILES) $(XML_APPLICATION_FILES)

# ----------------------------------------------------

HTML_FILES = $(XML_APPLICATION_FILES:%.xml=$(HTMLDIR)/%.html) \
	$(XML_PART_FILES:%.xml=$(HTMLDIR)/%.html) \
	$(GIF_FILES:%.gif=$(HTMLDIR)/%.gif)

INFO_FILE = ../../info

MAN3_FILES = $(XML_REF3_FILES:%.xml=$(MAN3DIR)/%.3)
MAN6_FILES = $(XML_REF6_FILES:%_app.xml=$(MAN6DIR)/%.6)

HTML_REF_MAN_FILE = $(HTMLDIR)/index.html

TOP_PDF_FILE = $(PDFDIR)/$(APPLICATION)-$(VSN).pdf

SPECS_FILES = $(XML_REF3_FILES:%.xml=$(SPECDIR)/specs_%.xml)

TOP_SPECS_FILE = specs.xml

# ----------------------------------------------------
# FLAGS 
# ----------------------------------------------------
XML_FLAGS += 

SPECS_FLAGS = -I../../include -I../../../kernel/include

# ----------------------------------------------------
# Targets
# ----------------------------------------------------
$(HTMLDIR)/%.gif: %.gif
	$(INSTALL_DATA) $< $@

docs: man pdf html

$(TOP_PDF_FILE): $(XML_FILES)

pdf: $(TOP_PDF_FILE)

html: gifs $(HTML_REF_MAN_FILE)

man: $(MAN3_FILES) $(MAN6_FILES)

gifs: $(GIF_FILES:%=$(HTMLDIR)/%)

debug opt: 

clean clean_docs:
	rm -rf $(HTMLDIR)/*
	rm -f $(MAN3DIR)/*
	rm -f $(MAN6DIR)/*
	rm -f $(TOP_PDF_FILE) $(TOP_PDF_FILE:%.pdf=%.fo)
	rm -f $(SPECDIR)/*
	rm -f errs core *~ 

$(SPECDIR)/specs_erl_id_trans.xml:
	escript $(SPECS_EXTRACTOR) $(SPECS_FLAGS) \
		-o$(dir $@) -module erl_id_trans

# ----------------------------------------------------
# Release Target
# ---------------------------------------------------- 
include $(ERL_TOP)/make/otp_release_targets.mk

release_docs_spec: docs
	$(INSTALL_DIR) $(RELSYSDIR)/doc/pdf
	$(INSTALL_DATA) $(TOP_PDF_FILE) $(RELSYSDIR)/doc/pdf
	$(INSTALL_DIR) $(RELSYSDIR)/doc/html
	$(INSTALL_DATA) $(HTMLDIR)/* \
		$(RELSYSDIR)/doc/html
	$(INSTALL_DATA) $(INFO_FILE) $(RELSYSDIR)
	$(INSTALL_DIR) $(RELEASE_PATH)/man/man3
	$(INSTALL_DATA) $(MAN3DIR)/* $(RELEASE_PATH)/man/man3
	$(INSTALL_DIR) $(RELEASE_PATH)/man/man6
	$(INSTALL_DATA) $(MAN6_FILES) $(RELEASE_PATH)/man/man6

release_spec:
