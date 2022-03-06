DEFENDER_DIR := ..
DEFENDER_BIN_DIR := $(DEFENDER_DIR)/bin
RED_LABEL := $(DEFENDER_DIR)/redlabel

TMP_DIR := bin
SRC_DIR := .
OUT_DIR := redlabel

GASM_DIR := ../../glht/target/debug/

COMMON_SRC := macros.68 memory.src

CMP := ./cmpfiles $(RED_LABEL) $(OUT_DIR)

ASM := $(GASM_DIR)/gasm --star-comments --max-errors 50 --mem-size 94208\
		--set OUT_DIR $(OUT_DIR) \
		--set TMP_DIR $(TMP_DIR) \
		--set RED_LABEL $(RED_LABEL) \
		$(foreach src,$(COMMON_SRC), $(SRC_DIR)/$(src))

DEFA_SRC :=     defa.src

DEFA_ROMS :=    defend.1 \
	            defend.2 \
	            defend.3 \
	            defend.4 \
	            defend.9 \
	            defend.11 \
	            defend.12

ROMS_SRC :=     roms.src

ROMS_ROMS :=    defend.6 \
	            defend.7 \
				defend.8 \
	            defend.10

ALL_ROMS :=     $(ROMS_ROMS) $(DEFA_ROMS)

ROMS_ROMS_FULL := $(foreach rom, $(ROMS_ROMS), $(OUT_DIR)/$(rom))
ROMS_SRC_FULL := $(foreach src, $(ROMS_SRC), $(SRC_DIR)/$(src))
DEFA_ROMS_FULL := $(foreach rom, $(DEFA_ROMS), $(OUT_DIR)/$(rom))
DEFA_SRC_FULL := $(foreach src, $(DEFA_SRC), $(SRC_DIR)/$(src))

ALL_ROMS_FULL := $(ROMS_ROMS_FULL) $(DEFA_ROMS_FULL) 

all: dirs roms
	@echo done

dirs:
	-@mkdir -p $(TMP_DIR) $(OUT_DIR)
	@echo Made Directories

$(DEFA_ROMS_FULL): $(DEFA_SRC_FULL)
	@echo Building $<
	@$(ASM) $< -s $(TMP_DIR)/$(notdir $<).sym

$(ROMS_ROMS_FULL): $(ROMS_SRC_FULL)
	@echo Building $<
	@$(ASM) $< -s $(TMP_DIR)/$(notdir $<).sym

clean:
	@rm -rf $(OUT_DIR) $(TMP_DIR)
	@echo Cleaned

cmp:
	@echo 
	@echo Comparing ROMS
	@for rom in $(ALL_ROMS) ; do \
		$(CMP) $$rom  ;\
	done

roms: $(ALL_ROMS_FULL) cmp
	@echo Built ROMS
