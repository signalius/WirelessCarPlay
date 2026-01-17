CC      := gcc
TARGET  := AppleCarPlay

SRC     := AppleCarPlay_AppStub.c
PLAT_SRCS := $(wildcard ../Platform/*.c)

CFLAGS  := -fPIC \
           -I../Sources \
           -I../AccessorySDK/Support/ \
           -I../build/Release-linux/ \
           -I../Support \
           -I../Platform

LDFLAGS := -L. \
           -L../build/Release-linux/ \
           -L../../mDNSResponder/mDNSPosix/build/prod

LDLIBS  := -lpthread \
           -lAirPlay \
           -lAirPlaySupport \
           -lAudioConverter \
           -lScreenStream \
           -lAudioStream \
           -ldns_sd \
           -lCoreUtils \
           -ldns_sd

.PHONY: all clean

all: $(TARGET)

$(TARGET): $(SRC) $(PLAT_SRCS)
	$(CC) $(SRC) $(PLAT_SRCS) $(LDFLAGS) $(LDLIBS) $(CFLAGS) -o $@

clean:
	rm -f $(TARGET)

