# Run tests
#
# Copyright (c) 2011-2012 Mathias Lafeldt
# Copyright (c) 2005-2012 Git project
# Copyright (c) 2005-2012 Junio C Hamano
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see http://www.gnu.org/licenses/ .

SHELL_PATH = $(SHELL)
RM = rm -f
PROVE = prove
AGGREGATE_SCRIPT = aggregate-results.sh

export SHELL_PATH

T = $(sort $(wildcard *.t))

test: pre-clean
	$(MAKE) aggregate-results-and-cleanup

prove: pre-clean
	@echo "*** prove ***"; $(PROVE) --exec '$(SHELL_PATH)' $(PROVE_OPTS) $(T) :: $(TEST_OPTS)
	$(MAKE) clean-except-prove-cache

$(T):
	@echo "*** $@ ***"; '$(SHELL_PATH)' $@ $(TEST_OPTS)

pre-clean:
	$(RM) -r "$${SHARNESS_TEST_OUTDIR-.}"/test-results

clean-except-prove-cache:
	$(RM) -r "$${SHARNESS_TEST_OUTDIR-.}"/'trash directory'.*
	$(RM) -r "$${SHARNESS_TEST_OUTDIR-.}"/test-results

clean: clean-except-prove-cache
	$(RM) .prove

aggregate-results-and-cleanup: $(T)
	$(MAKE) aggregate-results
	$(MAKE) clean

aggregate-results:
	@'$(SHELL_PATH)' '$(AGGREGATE_SCRIPT)'

.PHONY: test prove $(T) pre-clean clean
.PHONY: aggregate-results-and-cleanup aggregate-results
