PROJECT_NAME                            := $(notdir $(PWD))
PYTHON3                                 := $(shell which python3)
export PYTHON3
ifeq ($(port),)
PORT                                    := 8383
else
PORT                                    := $(port)
endif
export PORT

.PHONY: -
-: docs

.PHONY: report
report:
	@echo 'PROJECT_NAME=${PROJECT_NAME}'

.PHONY: docs
##:	docs                 build docs from sources/*.md
docs:
	ln -sF README.md COLDCARD-BlackBox.md
	#brew install pandoc
	bash -c "if hash pandoc 2>/dev/null; then echo; fi || brew install pandoc"
	bash -c 'pandoc -s 01-COLDCARD.md       -o 01-COLDCARD.html  --metadata title="" '
	bash -c 'pandoc -s 02-Blackbox.md       -o 02-Blackbox.html  --metadata title="" '
	bash -c 'pandoc -s 03-Slushpool.md      -o 03-Slushpool.html  --metadata title="" '
	bash -c 'pandoc -s 04-SparrowWallet.md  -o 04-SparrowWallet.html  --metadata title="" '
	bash -c 'pandoc -s COLDCARD-Blackbox.md -o COLDCARD-Blackbox.html  --metadata title="" '
	ln -sF COLDCARD-Blackbox.html index.html
	git add --ignore-errors *.md
	git add --ignore-errors assets
	git add --ignore-errors *makefile


.PHONY: serve
##:	serve                serve repo on $(PORT)
serve: docs
#REF: https://docs.python.org/3/library/http.server.html
	# bash -c "$(PYTHON3) -m http.server $(PORT) --bind 127.0.0.1 -d $(PWD) || open http://127.0.0.1:$(PORT)"
	$(PYTHON3) -m http.server $(PORT) --bind 127.0.0.1 -d $(PWD) > /dev/null 2>&1 || open http://127.0.0.1:$(PORT)
