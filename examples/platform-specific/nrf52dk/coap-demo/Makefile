CONTIKI=../../../..

ifeq ($(MAKECMDGOALS),)
$(error Please specify whether coap-client or coap-server should be built)
endif

ifneq ($(filter coap-client coap-client.flash, $(MAKECMDGOALS)),)
ifeq ($(SERVER_IPV6_ADDR),)
$(error Please define SERVER_IPV6_ADDR=<full ipv6 addr>)
else
CFLAGS += -DSERVER_IPV6_ADDR=\"$(SERVER_IPV6_ADDR)\"
CFLAGS += -DDEVICE_NAME=\"nRF52_DK_CoAP_Client\"
endif
else
CFLAGS += -DDEVICE_NAME=\"nRF52-DK-CoAP-Server\"
endif

# automatically build RESTful resources
REST_RESOURCES_DIR = ./resources
REST_RESOURCES_FILES = $(notdir $(shell find $(REST_RESOURCES_DIR) -name '*.c' ! -name 'res-plugtest*'))

PROJECTDIRS += $(REST_RESOURCES_DIR)
PROJECT_SOURCEFILES += $(REST_RESOURCES_FILES)

# REST Engine shall use Erbium CoAP implementation
MODULES += os/net/app-layer/coap

MAKE_ROUTING = MAKE_ROUTING_NONE

include $(CONTIKI)/Makefile.include
