DIST := dist

REVEAL_VERSION := 5.2.1
MATHJAX_VERSION := 3.2.2

REVEAL_CDN := https://cdn.jsdelivr.net/npm/reveal.js@$(REVEAL_VERSION)
MATHJAX_CDN := https://cdn.jsdelivr.net/npm/mathjax@$(MATHJAX_VERSION)

.PHONY: all clean serve

all: bundle

bundle: \
	$(DIST)/reveal/dist/reveal.css \
	$(DIST)/reveal/dist/reveal.js \
	$(DIST)/reveal/dist/theme/white.css \
	$(DIST)/reveal/plugin/math/math.js \
	$(DIST)/mathjax/tex-svg.js \
	$(DIST)/index.html

#
# Diretórios
#

$(DIST):
	mkdir -p $(DIST)

$(DIST)/reveal/dist/theme:
	mkdir -p $@

$(DIST)/reveal/plugin/math:
	mkdir -p $@

$(DIST)/mathjax:
	mkdir -p $@

#
# Arquivos Reveal.js
#

$(DIST)/reveal/dist/reveal.css: | $(DIST)/reveal/dist/theme
	curl -fsSL $(REVEAL_CDN)/dist/reveal.css -o $@

$(DIST)/reveal/dist/reveal.js: | $(DIST)/reveal/dist/theme
	curl -fsSL $(REVEAL_CDN)/dist/reveal.js -o $@

$(DIST)/reveal/dist/theme/white.css: | $(DIST)/reveal/dist/theme
	curl -fsSL $(REVEAL_CDN)/dist/theme/white.css -o $@

$(DIST)/reveal/plugin/math/math.js: | $(DIST)/reveal/plugin/math
	curl -fsSL $(REVEAL_CDN)/plugin/math/math.js -o $@

#
# MathJax
#

$(DIST)/mathjax/tex-svg.js: | $(DIST)/mathjax
	curl -fsSL $(MATHJAX_CDN)/es5/tex-svg.js -o $@

#
# HTML
#

$(DIST)/index.html: index.html | $(DIST)
	cp $< $@

#
# Servidor
#

serve: bundle
	cd $(DIST) && python3 -m http.server 8000

#
# Limpeza
#

clean:
	rm -rf $(DIST)
