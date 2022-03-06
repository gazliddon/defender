# Phonies
.PHONY: all clean dirs cmp roms

# Locations
DEFENDER_DIR     := ..
DEFENDER_BIN_DIR := $(DEFENDER_DIR)/bin
RED_LABEL        := $(DEFENDER_DIR)/redlabel

TMP_DIR := bin
SRC_DIR := .
OUT_DIR := redlabel
DEPS_DIR := deps
GASM_DIR := ../../glht/target/debug/

# Tools
CMP := ./cmpfiles $(RED_LABEL) $(OUT_DIR)
ASM := $(GASM_DIR)/gasm --star-comments --max-errors 50 --mem-size 94208 \
		--set OUT_DIR $(OUT_DIR) \
		--set TMP_DIR $(TMP_DIR) \
		--set RED_LABEL $(RED_LABEL)

# Inputs
COMMON_SRC := macros.68 memory.src
SRCS       := roms.src defa.src

# Outputs
ROMS :=     defend.1 \
			defend.2 \
			defend.3 \
			defend.4 \
			defend.6 \
			defend.7 \
			defend.8 \
			defend.9 \
			defend.10 \
			defend.11 \
			defend.12

# Expansions
SYMS := $(SRCS:%.src=$(TMP_DIR)/%.sym)
DEPS := $(SRCS:%.src=$(DEPS_DIR)/%.d)

# Assemble src file and create deps file
$(TMP_DIR)/%.sym : $(SRC_DIR)/%.src
	@echo Assembling $< to $@
	@$(ASM) \
	$(COMMON_SRC:%.c=$(SRC_DIR)/%.c) \
	$< -s $@ --deps $(DEPS_DIR)/$*.d

# Rules
all: dirs roms cmp
	@echo done

dirs:
	-@mkdir -p $(TMP_DIR) $(OUT_DIR) $(DEPS_DIR)
	@echo Made Directories

cmp:
	@echo Comparing ROMS
	@for rom in $(ROMS) ; do \
		$(CMP) $$rom  ;\
	done

roms: $(SYMS) $(foreach rom, $(ROMS), $(OUT_DIR)/$(rom)) 
	@echo Built ROMS

clean:
	@rm -rf $(OUT_DIR) $(TMP_DIR) $(DEPS_DIR)
	@echo Cleaned


-include $(DEPS)
