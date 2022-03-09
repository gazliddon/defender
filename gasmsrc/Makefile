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
GASM_DIR := ../../gazm/target/release

# Tools
CMP := ./cmpfiles $(RED_LABEL) $(OUT_DIR)
ASM := $(GASM_DIR)/gazm --star-comments --max-errors 50 --mem-size 94208 \
		--set OUT_DIR $(OUT_DIR) \
		--set TMP_DIR $(TMP_DIR) \
		--set RED_LABEL $(RED_LABEL)

# Inputs
COMMON_SRC := macros.68 memory.src
SRCS       := roms.src

# If the redlabel reference roms exist then include 
# a file that'll load them in to reference compilation against
ifeq ($(wildcard $(RED_LABEL)/*),)
else
	COMMON_SRC := $(COMMON_SRC) refroms.src
endif

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
	@$(ASM) $(COMMON_SRC:%.c=$(SRC_DIR)/%.c)  $< -s $@ --deps $(DEPS_DIR)/$*.d

# Rules
all: dirs roms cmp
	@echo done

dirs:
	-@mkdir -p $(TMP_DIR) $(OUT_DIR) $(DEPS_DIR)
	@echo Made Directories

roms: $(SYMS) $(foreach rom, $(ROMS), $(OUT_DIR)/$(rom)) 
	@echo Built ROMS

clean:
	@rm -rf $(OUT_DIR) $(TMP_DIR) $(DEPS_DIR)
	@echo Cleaned

-include $(DEPS)

cmp: 
	@echo CSUMing ROMS
	@./checksumroms \
	59fa9a3a3939a2edc939c89925b89cb1ee9750680976e3d24dea3349079e1969  $(OUT_DIR)/defend.1 \
	9a51272a8f931d9df6222eeb4db57a60abd658c81753a6551095441edb0bac9c  $(OUT_DIR)/defend.10 \
	ad1ba89c0ea561ef6c1c58951c3bf1d98a5316823e601f9ce92866c1ea6006c8  $(OUT_DIR)/defend.11 \
	0ce61122822e2a4a58a444bff13979fe2fb2024016ed0ea48adb6a34d9e38f3d  $(OUT_DIR)/defend.12 \
	14232d72b80de954e95a2b3ca093903da18d739cce9e396ab258d3be44e31452  $(OUT_DIR)/defend.2 \
	6b710587e1e7ed8429ac027279b2c2d16366149599262085b8e6efb4588790d4  $(OUT_DIR)/defend.3 \
	311777edf0ba369b4b6a25a0988856be07986096766713df97df25ac10fc4e9c  $(OUT_DIR)/defend.4 \
	8a28cda37da2e009894a68e6b3bbb76c49e409e81788aa71b404656b9b600d58  $(OUT_DIR)/defend.6 \
	acbb5db53da6bc93a7e8dd66761c89dc34d49fab177b28328d7bb1aef66fed59  $(OUT_DIR)/defend.7 \
	522fafb3edb07a22f6868c01d5847f9176f290847ded63f01363b1b080fe71f2  $(OUT_DIR)/defend.8 \
	1af04bafe593e4a117333cd878376567cc6a70cbe41cb416c1722595885a7c5b  $(OUT_DIR)/defend.9
	@echo testing done

