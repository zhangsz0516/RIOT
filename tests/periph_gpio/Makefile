include ../Makefile.tests_common

FEATURES_REQUIRED = periph_gpio
FEATURES_OPTIONAL = periph_gpio_irq

USEMODULE += shell
USEMODULE += shell_commands
USEMODULE += benchmark

# disable native GPIOs for automatic test
ifeq (native,$(BOARD))
  USEMODULE += periph_gpio_mock
endif

BOARDS_BENCH_PORT_1 = \
    slstk3402a \
    z1 \
    #

# port 0 pins are used for serial output on these boards, e.g.: on slstk3402a
# PA5 (or port 0, pin 5) is used to control the BC enabling serial output,
# therefore test on port 1.
ifneq (,$(filter $(BOARD),$(BOARDS_BENCH_PORT_1)))
  PORT_UNDER_TEST ?= 1
else
  PORT_UNDER_TEST ?= 0
endif

include $(RIOTBASE)/Makefile.include

$(call target-export-variables,test,PORT_UNDER_TEST)

bench:
	tests/02-bench.py
