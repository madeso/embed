set(src
    embed/types.cc embed/types.h
)
add_library(embed STATIC ${src})
target_include_directories(embed
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
)
if(NOT EMBED_MASTER_PROJECT)
    set_target_properties(embed PROPERTIES FOLDER "External/Embed")
endif()
add_library(embed::embed ALIAS embed)

