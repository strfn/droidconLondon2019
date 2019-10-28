# Unit Test your View Workshop 1
dependency injection Koin
View orchestration: roboelectic
code repos: https://github.com/jdortiz/TeaRank
create new test: select class and hit CMD-Shift-T
Use Junit4, Junit5 is not ready yet to work with roboelectict. If using Junit5 there is an option to say at runtime to switch to junit4 for some testing

As a destination of the test do not select AndroidTest but src/test. THe AndroidTest folder use default instrumentaiton which is slower we want instead to use roboelectric


# MotionLayout
Based on motioscene is an xml in the res folder that describe the scene.
Constraint in the transition overrides the constraints defined in the view
Android studio has a visual editor for the transcitions.
RecycleView and List needs some code 
__CHECK LAST PART OF THE RECORDING FOR LINKS TO PRESENTATION AND CODE REPO__

https://mikescamell.com
https://github.com/mikescamell/Loco-MotionLayout

# Companies
- Protectmyapp, injects anti tempering technologies into the packaged application, they have a more advanced inhouse tool which is cabaple of inspecting the app and add extra layer of security like for example ensure a pinned certificate is not swapped at runtime, for data at rest they add an extra layer of encryption tight to the device.
- crashlytics, importing crashlytics into the project import only the bare minumum firebase components in order to work, tracking of the user can be disabled via a property. reach pout to crashlytics support to get any more details like GDPR encryption and what data is collected.
- bitrise: CI/CD platform is mostly hosted but they have onprem solution in the pipeline (should not be publicly available yet), feature flag support in the roadmap. handed over contact and they will reach out for further discusison.
- 

# Overview of Biometric Auth
Legacy API 23+ was for fingerprint
FingerprintManager, reuires permission in the manifest
1. isHardwareDetected (if device was built before 23 but still had fingerprint it returns false, user might complain as they have fingerprint but the app not support it, not much you can do)
1. do not use hasSystemFeature(FEATURE_FINGERPRINT) as unrealible
1. check if hasEnrolledFingerprints __call only if you have detected hardware otherwise might throw exception__
1. authneticate do not provide UI it only starts the sensor, you have to provide the UI, exception devices with onscreen sensor which automatically pops some UI, no way to detect that so might have weired situation where both teh device and the custom UI is on screen,
1. if app goes in background you need to cancel the manager
1. Crypto object __is the core of security for biometric__ is what holds the secret if not used corerctly the app won't be effectively secured. Signature used to comunicate with the server, chpher if you want to encrypt on the device.
1. Callback
   - authentication failed is not terminal, the user can re-try.
   - authenticvationhelp ask to show an help message to the user
1. AuthenticationResult the result contains the same crypto object pased in input, is valid only in the context of the success callback, it gets locked after so needs to be used straight away.

## AndroidX Fingerprintmanagercompact
 is a wrapper to the previous API it basically does the HW check automatically.
## API 28+ Biometric prompt api 
biggest difference is that it provides a system UI, BuimetricsPrompt.builder is used to prepare the UI.
The HW check is done BiometricManager.canAuthenticate() (__29+__)

## androidx.biometric
is API 14+ still in rc but is unifying the behaviour and trying to take care of the variation.

## CryptoOject 
Ensure you have a good crash reporting as they can easily crash.

KeyGenerator: 
keygenerator.init:
- setUserAuthenticationRequired(true) --> __IF NOT SET NO REAL SECURITY IS APPLIED AS THE CRYPTO IS ALWAYS UNLOCKED__
- setInvalidatedBybiometricEnrollment(true) it invalidates teh key is new finder is added or edit

Keugenerator.generate() to generate the key and put in the store.
Check security key attestation in developer.android.com/training/articles

# Designed an Intent-based API
If start building libraries consider using intents ad a means of comunication between the library and the consumer. Intents are system wide and supported basically by any platfomr (native, hybrid, cross ....)

# get over certs pinning.
Cert pining is based on trust of the root certificate (root authorities can be hacked so don't trust)

A lot of things to consider if doing cert pinning, for example how you refresh a cert if is leaked.
## Certificate trasparency 
certificate issuing logged publicly so can be verified
check video the very best of certificate trasparancy network@scale2017

based on monitoring certificate issues for your domain.
client verification 
in ios ATS requirescertificatetrasparency
Android: babylon opensourced certificate trasparency library 
https://www.certificate-transparency.org

# Keynote, get happy get known get paid












