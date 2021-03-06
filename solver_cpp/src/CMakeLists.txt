IF (FLUID_TEST)
    SET(TFLUIDS
         fluidnet_implementation/init.cpp
         fluidnet_implementation/advect_type.cpp
       )
ELSE ()
    SET(TFLUIDS )
ENDIF()

SET(GRID
     grid/bool_conversion.cpp
     grid/grid.cpp
    )
SET(ADVECTION
     advection/advection.cpp
     advection/advect_type.cpp
     advection/calc_line_trace.cpp
   ) 
SET(BCS
     boundaryCondition/bcs.cpp
   )
SET(STERMS
     sourceTerms/source_term.cpp
   )
SET(PROJECTION
     projection/div.cpp
     projection/solve_linear_sys.cpp
     projection/update_vel.cpp
   )
ADD_LIBRARY(FluidNet SHARED ${TFLUIDS} ${GRID} ${ADVECTION} ${ADVECTION_OLD} ${BCS} ${STERMS} ${PROJECTION})
TARGET_INCLUDE_DIRECTORIES(FluidNet
   PUBLIC
       $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/grid;
       ${CMAKE_CURRENT_SOURCE_DIR}/advection;
       ${CMAKE_CURRENT_SOURCE_DIR}/boundaryCondition;
       ${CMAKE_CURRENT_SOURCE_DIR}/sourceTerms;
       ${CMAKE_CURRENT_SOURCE_DIR}/projection;
       ${CMAKE_CURRENT_SOURCE_DIR}/fluidnet_implementation;
       ${CMAKE_CURRENT_SOURCE_DIR}
       >
)

