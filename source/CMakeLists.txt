set(Adamantine_HEADERS
    ${CMAKE_CURRENT_SOURCE_DIR}/ElectronBeam.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/Geometry.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/ImplicitOperator.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/MaterialProperty.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/NewtonSolver.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/Operator.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/Physics.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/PostProcessor.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/ThermalOperator.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/ThermalPhysics.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/Timer.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/utils.hh
    ${CMAKE_CURRENT_SOURCE_DIR}/types.hh
  )
set(Adamantine_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/ElectronBeam.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/Geometry.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/ImplicitOperator.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/MaterialProperty.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/NewtonSolver.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/PostProcessor.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/ThermalOperator.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/ThermalPhysics.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/Timer.cc
  )

# Because the Adamantine library is just used to simplify testing, we make it
# static. Thus, once the application is created it can be moved around. The
# other libraries can still be shared.
add_library(Adamantine STATIC ${Adamantine_SOURCES})

DEAL_II_SETUP_TARGET(Adamantine)

set_target_properties(Adamantine PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

target_link_libraries(Adamantine Boost::boost)
target_link_libraries(Adamantine Boost::chrono)
target_link_libraries(Adamantine Boost::filesystem)
target_link_libraries(Adamantine Boost::program_options)
target_link_libraries(Adamantine MPI::MPI_CXX)
target_include_directories(Adamantine PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
