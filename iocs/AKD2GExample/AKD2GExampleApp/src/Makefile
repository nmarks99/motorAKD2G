TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

# PROD_NAME is used by ADCORE to add libraries
# DBD_PREFIX is used by ADCORE to add dbd files
PROD_NAME = AKD2GExample
DBD_PREFIX = iocAKD2GExample
PROD_IOC = $(PROD_NAME)

# Note that the order in which .dbd files and libraries are added to a list
# variable is important.  For .dbd files, things must be defined before they
# are referenced by a later .dbd file.  For libraries, things must be referenced
# before they are searched for; otherwise they won't be included.

##################################################################
# First, define $(DBD_NAME)_DBD and $(PROD_NAME)_LIBS from the modules
# defined in RELEASE
##################################################################
DBD_SUFFIX_Linux = Linux
DBD_SUFFIX_WIN32 = Win$(if $(findstring 32, $(T_A)),32,64)
DBD_NAME = $(DBD_PREFIX)$(DBD_SUFFIX_$(OS_CLASS))

DBD  += $(DBD_NAME).dbd

$(DBD_NAME)_DBD += base.dbd

ifdef AKD2G
  $(DBD_NAME)_DBD += akd2gSupport.dbd
  $(PROD_NAME)_LIBS := akd2g $($(PROD_NAME)_LIBS)
endif

ifdef ASYN
  $(DBD_NAME)_DBD += asyn.dbd
  $(DBD_NAME)_DBD += drvAsynSerialPort.dbd drvAsynIPPort.dbd drvVxi11.dbd devGpib.dbd
  $(PROD_NAME)_LIBS := asyn $($(PROD_NAME)_LIBS)
endif

ifdef MOTOR
  $(DBD_NAME)_DBD += motorSupport.dbd
  $(PROD_NAME)_LIBS := motor $($(PROD_NAME)_LIBS)
endif

# ifdef MOTOR
  # $(DBD_NAME)_DBD += motorSupport.dbd devAcsMotor.dbd devAerotech.dbd
  # $(DBD_NAME)_DBD += devAttocube.dbd devFaulhaberMotor.dbd devImsMotor.dbd
  # $(DBD_NAME)_DBD += devKohzuMotor.dbd devMclennanMotor.dbd devMicos.dbd
  # $(DBD_NAME)_DBD += devMicroMo.dbd devNewFocus.dbd devNewport.dbd
  # ifdef SNCSEQ
  # $(DBD_NAME)_DBD += devAerotechSeq.dbd devNewportSeq.dbd
  # endif
  # $(DBD_NAME)_DBD += devOriel.dbd devPC6K.dbd devPIJena.dbd devPIMotor.dbd
  # $(DBD_NAME)_DBD += devSPiiPlus.dbd devSmartMotorMotor.dbd devSoftMotor.dbd
  # $(DBD_NAME)_DBD += devThorLabs.dbd motorSimSupport.dbd
#
  # $(PROD_NAME)_LIBS := motor $($(PROD_NAME)_LIBS)
  # $(PROD_NAME)_LIBS := Acs acsTech80 Aerotech Attocube Faulhaber Ims KohzuMotor $($(PROD_NAME)_LIBS)
  # $(PROD_NAME)_LIBS := Mclennan Micos MicroMo NewFocus Newport Oriel PI PIJena $($(PROD_NAME)_LIBS)
  # $(PROD_NAME)_LIBS := Parker SmartMotor ThorLabs softMotor motorSimSupport $($(PROD_NAME)_LIBS)
# endif

$(PROD_NAME)_LIBS += $(EPICS_BASE_IOC_LIBS)

# <name>_registerRecordDeviceDriver.cpp will be created from <name>.dbd
$(PROD_NAME)_SRCS  += $(DBD_NAME)_registerRecordDeviceDriver.cpp $(PROD_NAME)Main.cpp

#===========================

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE
