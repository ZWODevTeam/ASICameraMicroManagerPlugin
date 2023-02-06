include ../rules.mk



ASICam2:  SequenceThread.o MyASICam2.o

ifeq ($(APPLE), 0)
ifeq ($(dy), dy)
	$(CC) $(CFLAGS) $(DEFS) -shared -Wall -o libmmgr_dal_ASICam2.so MyASICam2.o  SequenceThread.o -lcommon -lASICamera2 -L../MMDevice -L../../linux/lib/$(platform) 
else
	$(CC) $(CFLAGS) $(DEFS) -shared -Wall -o libmmgr_dal_ASICam2.so MyASICam2.o  SequenceThread.o -lcommon ../../linux/lib/$(platform)/libASICamera2.a ../../../EFW/FilterSDK/lib/$(platform)/libEFWFilter.a -L../MMDevice
endif
	cp -f libmmgr_dal_ASICam2.so ../../linux/uManager/$(platform)/$(dy)/libmmgr_dal_ASICam2.so.$(VERSION)
	ln -sf libmmgr_dal_ASICam2.so.$(VERSION) ../../linux/uManager/$(platform)/$(dy)/libmmgr_dal_ASICam2.so.0
else

ifeq ($(dy), dy)
	$(CC) $(CFLAGS) $(DEFS) -dynamiclib -Wall -current_version $(VERSION) -compatibility_version 1.0.0 -o libmmgr_dal_$(sdkname) MyASICam2.o  SequenceThread.o -lcommon -l$(sdkname) -L../MMDevice -L../../linux/lib/$(platform) 
else
	$(CC) $(CFLAGS) $(DEFS) -dynamiclib -Wall -current_version $(VERSION) -compatibility_version 1.0.0 -o libmmgr_dal_$(sdkname) MyASICam2.o  SequenceThread.o -lcommon ../../linux/lib/$(platform)/lib$(sdkname).a ../../../EFW/FilterSDK/lib/$(platform)/libEFWFilter.a -L../MMDevice 
endif
ifeq ($(FakeUSB), n)
	install_name_tool -change /usr/local/lib/libusb-1.0.0.dylib @loader_path/libusb-1.0.0.dylib libmmgr_dal_$(sdkname)
endif
	cp -f libmmgr_dal_$(sdkname) ../../linux/uManager/$(platform)/$(dy)/

endif

MyASICam2.o:
	$(CC) -c $(CFLAGS) $(DEFS) MyASICam2.cpp -I../MMDevice -I../../ASICamera -I../../../EFW/FilterSDK/EFW_filter 
SequenceThread.o:
	$(CC) -c $(CFLAGS) $(DEFS) SequenceThread.cpp -I../MMDevice -I../../ASICamera -I../../../EFW/FilterSDK/EFW_filter
clean :
	rm *.o *.dylib *so libmmgr*

