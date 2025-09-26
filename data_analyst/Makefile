# ------------------- configurable knobs -------------------
CONTAINER_NAME ?= metabase
DATA_DIR       ?= $(CURDIR)/data
MB_DATA_DIR    ?= $(CURDIR)/metabase-data
PORT           ?= 3002

# ----------------------------------------------------------
.PHONY: up

up:          ## Start Metabase (foreground with auto-cleanup)
	docker run --rm --name $(CONTAINER_NAME) \
		-p $(PORT):3000 \
		-v $(MB_DATA_DIR):/metabase-data \
		-v $(DATA_DIR):/data \
		-e MB_DB_FILE=/metabase-data/metabase.db \
		metabase/metabase
