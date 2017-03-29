# ePCSDataEntryForPrescriber
DEA e-Prescribing Code Setup and Configuration

Please go through this whole Readme file and follow the instructions accordingly. 

I will guide you step by step while configuring ePCSDataEntryForPrescriber code. I tested, installed and fixed code, path, and components using RAD Berlin 10.1 and RAD Tokyo 10.2. It should work with prior versions of Delphi Studios (Borland etc.) with some configuration changes.

1. Code Setup Instructions:

Note: Throughout these instructions do not forget to keep saving the projects before closing after 'successful' builds or installs. Feel free to delete Project files; package compile and build will generate new itself. You can always check successful installed components by clicking "Components -> Installed Packages" on main menu bar. Scroll all the way down to see or find your package name(s) here.

There will be four folders in ePCS folder:
 - Code (ePCSDataEntryForPrescriber actual code is in this folder)
    - Step 5: (Please go through Step 1-4 first if you haven’t already) 
        - Open ePCSDataEntryForPrescriber Studio Project File. Now right click on ePCSDataEntryForPrescriber project and click on Options.
        - Make sure 'DCP Output Directory' set to "[Your Directory]\ePCS\Code\Debug\"
        - Make sure 'Search Path' is set to "[Your Directory]\ePCS\Packages\XuDigSig;[Your Directory]\ePCS\Packages\Broker\Source;[Your Directory]\ePCS\Packages\FMDC\Driver"
        - Make sure 'Unit Output Directory' is set to "[Your Directory]\ePCS\Code\DCU\"
        - Right click on ePCSDataEntryForPrescriber project and click ‘Clean’, ‘Compile’ and then ‘Build’. 
        - Time to Run :) Hit F9 or click on the GREEN ARROW ;)
 - Documents (Short Technical Analysis)
 - Packages: There will be 4 following folders in this folder: 
    - Broker 
        - Step 1: Open XWB_RXE3 Delphi Package file. Right click on project and click ‘Clean’, ‘Compile’ and ‘Build’.
        - Step 2: Open XWB_DXE3 Delphi Package file. Right click on project and click ‘Clean’, ‘Compile’ and then ‘Build’. An extra step here would be right click again and now ‘Install’. It should display the following message in the pop-up "Package [Directory Path] has been installed. The following new component(s) have been registered: TContextorControlXWB_DXE3, TRPCBroker, TXWBRichEdit."
    - FMDC 
        - Step 3: Open FMDC Delphi Package. Right Click on FMDC Project and click on Options and set 'DCP Output Directory' and 'Unit Output Directory' to '[Your Directory]\ePCS\Packages\FMDC\Driver\DCU\
        - Step 4: Right click on project and click ‘Clean’, ‘Compile’ and then ‘Build’. An extra step here would be right click again and now ‘Install’. It should display the following message in the pop-up "Package [Directory Path] has been installed. The following new component(s) have been registered: TFMCheckBox, TFMComboBox, TFMComboBoxLookUp, TFMEdit, TFMFiler, TFMFinder, TFMFindOne, TFMGets, TFMHelp, TFMLabel, TFMListBox, TFMLister, TFMLookUp, TFMMemo, TFMRadioButton, TFMRadioGroup, TFMValidator."
    - PKI 
    - XuDigSig
 - Release: Set your ePCS project option to generate .exe in this folder.

2. Technical Details:

Context (option):	XU EPCS EDIT DATA		

Keys Required:                 ORES, XUEPCSEDIT	

Remote Procedures Calls (TAG^ROUTINE):	
  - XUS PKI SET UPN (SETUPN^XUSER2): Get SUBJECT ALTERNATIVE NAME for PIV card check. -p580
  - XU EPCS EDIT (ENTRY^XUEPCSED): RPC to handle EPCS data changes
  - XUS PKI GET UPN (GETUPN^XUSER2): Set the SUBJECT ALTERNATIVE NAME from the PIV card p580.					
Standard Remote Procedure Calls:
 - XUS KEY CHECK	: Key Check Routine - Standard (CPRS, Imaging, VOE, Vitals etc.)	
 - XWB GET VARIABLE VALUE	: FMDC Components Controls Code behind for retrieving data

Direct Global Reads	
 - $$SITE^VASITE()	
 - $G(^DIC(4,' + FacilityIen + ',"DEA"))	: Delphi Function: GetFacilityVANum	
