
cmake_minimum_required(VERSION 3.15)

project(JucePluginTemplate VERSION 0.0.1)

set (BaseTargetName SimpleEQ)

# find_package(JUCE CONFIG REQUIRED)      	# If you've installed JUCE to your system
# or
add_subdirectory(JUCE)                    		# If you've put JUCE in a subdirectory called JUCE


juce_add_plugin("${BaseTargetName}"
    # VERSION ...                               # Set this if the plugin version is different to the project version
    # ICON_BIG ...                              # ICON_* arguments specify a path to an image file to use as an icon for the Standalone
    # ICON_SMALL ...
    COMPANY_NAME "LionelDSP"
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT TRUE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    COPY_PLUGIN_AFTER_BUILD TRUE
    PLUGIN_MANUFACTURER_CODE Lion
    PLUGIN_CODE SEQ0                 
    FORMATS AU VST3 Standalone
    PRODUCT_NAME "Lionel DSP SimpleEQ")

# `juce_generate_juce_header` will create a JuceHeader.h for a given target, which will be generated into your build tree.
# This should be included with `#include <JuceHeader.h>`.
# The include path for this header will be automatically added to the target.
# The main function of the JuceHeader is to include all your JUCE module headers.

# juce_generate_juce_header(${BaseTargetName})

target_sources(${BaseTargetName}
    PRIVATE
        Source/PluginEditor.cpp
        Source/PluginProcessor.cpp)

target_compile_definitions(${BaseTargetName}
    PUBLIC
        JUCE_WEB_BROWSER=0
        JUCE_USE_CURL=0
        JUCE_VST3_CAN_REPLACE_VST2=0)

# juce_add_binary_data(AudioPluginData SOURCES ...)

target_link_libraries(${BaseTargetName}
    PRIVATE
        juce::juce_audio_utils
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)
