RUBY_COMMAND = ruby
GREGORIO = gregorio
LUALATEX = lualatex
SED = sed
AWK = awk
GREP = grep
CAT = cat
CP = cp
MV = mv
TMP_DIR = temporalia
ifneq ($(wildcard $(TMP_DIR)),$(TMP_DIR))
TD := $(shell mkdir $(TMP_DIR))
endif
EDITIO_ROOTDIR = ../..
TOOLS_DIR = $(EDITIO_ROOTDIR)/instrumenta
PSALMS_DIR = $(EDITIO_ROOTDIR)/psalmi/amon33
PSALMTONES_DIR = $(EDITIO_ROOTDIR)/tonipsalmorum/arom12
CZECH_PSALMS_DIR = $(EDITIO_ROOTDIR)/bohemice_psalmi
COMMON_CHANTS_DIR = $(EDITIO_ROOTDIR)/cantuscommunes
PSALM_PREPROCESSOR = $(TOOLS_DIR)/psalmpreprocessor.rb
INITIUM_TOOL = $(TOOLS_DIR)/initiumpsalmi.rb
PSSKIP = 1
GENPSCOMB = $(AWK) -f pscomb.awk -v PSSKIP=$(PSSKIP) -v TRFILE=$(word 2,$^) $< > $@
PSALMS = 1 2 3 4 8 10 18 20 23 44 45 62 66 86 90 92 95 96 97 99 109 110 111 112 116 118v_vi 118vii_viii 118ix_x 118xi_xii 118xiii_xiv 118xv_xvi 118xvii_xviii 118xix_xx 118xxi_xxii 121 126 133 145 146 147 148 149 150
include $(PSALMTONES_DIR)/tonus.mk
MODUS-1 = vi-F
MODUS-2 = i-a2
MODUS-3 = viii-g
MODUS-4 = viii-g
MODUS-8 = iv-A
MODUS-10 = i-g
MODUS-18 = iv-A
MODUS-20 = iv-E
MODUS-23 = iv-A
MODUS-44 = vii-c
MODUS-45 = vii-c
MODUS-62 = iii-a
MODUS-66 = dir
MODUS-86 = vii-c
MODUS-90 = viii-G
MODUS-92 = i-g
MODUS-95 = viii-G
MODUS-96 = vii-a
MODUS-97 = i-g
MODUS-99 = ii-D
MODUS-109 = i-g
MODUS-110 = ii-D
MODUS-111 = iii-a
MODUS-112 = i-D
MODUS-116 = ii-D
MODUS-118v_vi = vii-c
MODUS-118vii_viii = vii-c
MODUS-118ix_x = vii-c
MODUS-118xi_xii = vi-F
MODUS-118xiii_xiv = vi-F
MODUS-118xv_xvi = vi-F
MODUS-118xvii_xviii = vii-c
MODUS-118xix_xx = vii-c
MODUS-118xxi_xxii = vii-c
MODUS-121 = vi-F
MODUS-126 = viii-G
MODUS-133 = viii-G
MODUS-145 = iii-g
MODUS-146 = iv-E
MODUS-147 = v-a
MODUS-148 = v-a
MODUS-149 = v-a
MODUS-150 = v-a
MODUS-benedictus = visoll-F
MODUS-magnificat = isoll-D
MODUS-dan3 = iv-E
MODUSLIST = $(sort $(foreach P,$(PSALMS) benedictus magnificat dan3,$(MODUS-$(P))))
CZPSALMOPTS = --accents 0:0 --title-pattern " " --no-paragraph
CZPSALMS = $(patsubst %,$(TMP_DIR)/ps%-boh.tex,$(PSALMS))
ALLCZPSALMS = $(CZPSALMS) $(patsubst %,$(TMP_DIR)/%-boh.tex,benedictus magnificat dan3)
ALLCOMBPSALMS = $(patsubst $(TMP_DIR)/%-boh.tex,$(TMP_DIR)/%-comb.tex,$(ALLCZPSALMS))
GENPSALM = $(RUBY_COMMAND) $(PSALM_PREPROCESSOR) --output $@ $(PSALMOPTS) $< \
	   && $(SED) -i -e 's/\*/\\grestar{}/g' $@
TONUS = $(TONUS-$(MODUS-$*))
GLORIAPATRI = $(PSALMS_DIR)/gloriapatri.pslm
APPENDGLORIAPATRI = --append "`cat $(GLORIAPATRI)`"
LAPSALMOPTS_COMMON = --accents-style bold --flex-underline --skip-verses 1
LAPSALMOPTSACC = --accents $(word 1,$(TONUS)):$(word 3,$(TONUS)) \
		 --preparatory-syllables $(word 2,$(TONUS)):$(word 4,$(TONUS))
LAPSALMOPTS = $(LAPSALMOPTS_COMMON) $(LAPSALMOPTSACC)
LAPSALMS = $(patsubst %,$(TMP_DIR)/ps%.tex,$(PSALMS))
LAPSALMSEXTRA = $(patsubst %,$(TMP_DIR)/%.tex,benedictus magnificat dan3)
ALLLAPSALMS = $(LAPSALMS) $(LAPSALMSEXTRA)
SCORES = $(addprefix versus-,iustus) \
	 $(addprefix hym-,DiesVenit) \
	 $(addprefix benedicamus-solemnism-,1vesp 2vesp laud) \
	 $(addprefix deusinadiutorium-,communis solemnis alter) supplicatiolitaniae oratiodominica \
	 dominusvobiscum-solemnis domineexaudi $(addprefix magnificat-initium-,isoll-D visoll-F) \
	 $(addprefix capitulum-,AmplificatusEst ConsummatusIustus) \
	 oratio oratiodominica-mat benedicamus-minor \
	 $(addprefix absolutio-,exaudi ipsius avinculis) dominelabiamea \
	 $(addprefix benedictio-solemn-,benedictione unigenitus spiritus deus christus ignem evangelica divinum adsocietatem) \
	 $(addprefix ant-,adestdies carcernocte carnemterens cruorfusus dumgentiles exgestato gressusreddit hicdives \
			  iubaraltae laudantdominum laudemotus lausalmesit morbidisrefugium opugilegregie peremptorispena \
			  pertrimatum vivensabinfantia) \
	 $(addprefix resp-,castusmente laetabiturjustus) \
	 tonus-lectionis-solemnis \
	 benedicamus-solemnis-laud tedeum-solemnis tedeum-solemnis-gn tuautem \
	 ps112-initium-i-D ps116-initium-ii-D ps145-initium-iii-g ps146-initium-iv-E \
	 ps147-initium-v-a ps92-initium-i-g ps99-initium-ii-D ps62-initium-iii-a \
	 dan3-initium-iv-E benedictus-initium-visoll-F ps109-initium-i-g ps110-initium-ii-D \
	 ps111-initium-iii-e ps112-initium-iv-E
OTHERSCORES = $(patsubst %,$(TMP_DIR)/%.gtex,$(SCORES))
OTHERDEPS = $(TMP_DIR)/ps112iD.tex $(TMP_DIR)/ps116iiD.tex $(TMP_DIR)/ps145iiig.tex \
	    $(TMP_DIR)/magnificatiD.tex $(TMP_DIR)/ps99iiD.tex $(TMP_DIR)/ps62iiia.tex \
	    $(TMP_DIR)/ps110iiD.tex $(TMP_DIR)/ps111iiie.tex $(TMP_DIR)/ps112ivE.tex
LAPSALMSINITGABC = $(foreach P,$(PSALMS),$(TMP_DIR)/ps$(P)-initium-$(MODUS-$(P))-auto.gabc) \
		   $(foreach P,dan3 benedictus,$(TMP_DIR)/$(P)-initium-$(MODUS-$(P))-auto.gabc)
LAPSALMSINITTEX = $(patsubst %.gabc,%.gtex,$(LAPSALMSINITGABC))
GENINITIUM = cd $(TMP_DIR) && $(RUBY_COMMAND) ../$(INITIUM_TOOL) ../$(1) ../$(PSALMTONES_DIR)/$(2)-auto.gabc; \
	     [ $(2) = "dir" ] && cd .. && $(SED) -i -e '/(::)$$$$/{/(,) (::)$$$$/!{s/<b>//g;s/<\/b>//g}}' $(3) && cd $(TMP_DIR) || :; \
	     case "$(1)" in */ps118[ivx]*) cd .. && $(SED) -i -e 's/^( )/( )<v>\\hebinitial{'`$(AWK) -f hebletter.awk -v PSLM="$(1)"`'}<\/v>/' $(3);; esac || :
iter = $(patsubst %,iterator.mk,$(iter-left))
define iter-doit
$(TMP_DIR)/%-initium-$(i)-auto.gabc: $(PSALMS_DIR)/%.pslm $(PSALMTONES_DIR)/$(i)-auto.gabc; $(call GENINITIUM,$$<,$(i),$$@)
endef
iter-left := $(MODUSLIST)
include $(iter)
define iter-doit
$(TMP_DIR)/%.gtex: $(i)/%.gabc ; if $(GREP) -q ^nabc-lines: $$<; then $(SED) -e ':d;s/\(([^).]*\)\./\1/g;/([^)]*\./bd' $$<; else $(CAT) $$<; fi | $(SED) -e 's/<sp>\([AVR]\)\/<\/sp>\./<v>\\\1bardot{}<\/v>/g;s/†/ +/g;:d;s/\(([^)'\'']*\)'\''/\1/g;/([^)]*'\''/bd' | $(SED) -e ':d;s/\(\(^\|)\)[^(j]*\)j/\1i/g;s/\(\(^\|)\)[^(J]*\)J/\1I/g;td' | $(GREGORIO) -s -o $$@
endef
iter-left := . $(TMP_DIR) $(addprefix ../InNativitateBMV/cantus/,amon33 triplex76 nrom02) \
	     $(addprefix $(COMMON_CHANTS_DIR)/,kyriale76 amon33 arom12 lcantualis78) $(PSALMTONES_DIR) \
	     $(addprefix ../Epiphania/cantus/,arom12 grom61 cselecti57 triplex76) ../CorpusChristi ../InNativitateBMV
include $(iter)

all: wenceslai.pdf
$(TMP_DIR)/%.tex: PSALMOPTS = $(APPENDGLORIAPATRI) $(LAPSALMOPTS)
$(patsubst %,$(TMP_DIR)/%.tex,ps148 ps149 dan3): PSALMOPTS = $(LAPSALMOPTS)
$(TMP_DIR)/magnificat.tex $(TMP_DIR)/magnificatiD.tex: PSALMOPTS = $(APPENDGLORIAPATRI) --accents-style bold --flex-underline --skip-verses 2 $(LAPSALMOPTSACC)
$(TMP_DIR)/ps90.tex: PSALMOPTS = --accents-style bold --flex-underline $(LAPSALMOPTSACC)
$(patsubst %,$(TMP_DIR)/ps%.tex,118vii_viii 118ix_x 118xiii_xiv 118xv_xvi 118xix_xx 118xxi_xxii 133): PSALMOPTS = $(APPENDGLORIAPATRI) --accents-style bold --flex-underline $(LAPSALMOPTSACC)
$(TMP_DIR)/ps112iD.tex: TONUS = 2 0 1 3
$(TMP_DIR)/ps116iiD.tex: TONUS = 1 0 1 0
$(TMP_DIR)/ps145iiig.tex: TONUS = 2 0 1 1
$(TMP_DIR)/magnificatiD.tex: TONUS = 1 3 1 3
$(TMP_DIR)/ps99iiD.tex: TONUS = 1 0 1 0
$(TMP_DIR)/ps62iiia.tex: TONUS = 2 0 1 1
$(TMP_DIR)/ps110iiD.tex: TONUS = 1 0 1 0
$(TMP_DIR)/ps111iiie.tex: TONUS = 2 0 1 1
$(TMP_DIR)/ps112ivE.tex: TONUS = 1 2 1 3
$(TMP_DIR)/%-boh.tex: PSALMOPTS = $(CZPSALMOPTS)
$(CZPSALMS) $(TMP_DIR)/benedictus-boh.tex: $(TMP_DIR)/%-boh.tex: $(CZECH_PSALMS_DIR)/Hejcl1922/%.pslm
	$(GENPSALM)
$(TMP_DIR)/dan3-boh.tex: $(CZECH_PSALMS_DIR)/Pavlik/dan3.pslm
	$(GENPSALM)
$(patsubst %,$(TMP_DIR)/%-boh.tex, magnificat): $(TMP_DIR)/%-boh.tex: $(CZECH_PSALMS_DIR)/DMC199x/%.pslm
	$(GENPSALM)
$(LAPSALMS): $(TMP_DIR)/ps%.tex: $(PSALMS_DIR)/ps%.pslm
	$(GENPSALM)
	case "$<" in */ps118[ivx]*) $(AWK) -f hebletter.awk -v PSLM="$<" -v TEX=$(if $(filter --skip-verses,$(PSALMOPTS)),1,2) $@ > $@.tmp; $(MV) -f $@.tmp $@;; esac || :
	$(SED) -i -e 'y/Jj/Ii/' $@
$(LAPSALMSEXTRA): $(TMP_DIR)/%.tex: $(PSALMS_DIR)/%.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps62iiia.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps62.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps99iiD.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps99.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps110iiD.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps110.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps111iiie.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps111.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps112iD.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps112.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps112ivE.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps112.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps116iiD.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps116.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/ps145iiig.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/ps145.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(TMP_DIR)/magnificatiD.tex: \
$(TMP_DIR)/%.tex: $(PSALMS_DIR)/magnificat.pslm
	$(GENPSALM)
	$(SED) -i -e 'y/Jj/Ii/' $@
$(ALLCOMBPSALMS): $(TMP_DIR)/%-comb.tex: $(TMP_DIR)/%.tex $(TMP_DIR)/%-boh.tex
	$(GENPSCOMB)
$(TMP_DIR)/magnificat-comb.tex: PSSKIP = 2
wenceslai.pdf: wenceslai.tex conventuscommune.tex translationes_cs.tex \
	       $(ALLCZPSALMS) $(ALLLAPSALMS) $(ALLCOMBPSALMS) $(LAPSALMSINITTEX) $(OTHERSCORES) $(OTHERDEPS)
	$(LUALATEX) -interaction=nonstopmode $<
	$(LUALATEX) -interaction=nonstopmode $<
clean:
	-rm -rf $(TMP_DIR) *~ *.aux *.gaux *.greaux *.log
.PHONY: clean
