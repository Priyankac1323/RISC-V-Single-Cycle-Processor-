# Remaining modules for a 5-stage pipeline

These are pipeline-register and hazard-control building blocks. They are not a drop-in conversion of the earlier single-cycle CPU: the existing `processor_datapath.sv`, `control_unit.sv`, and `riscv_cpu.sv` must be redesigned and wired to these modules before the design becomes a functioning five-stage pipeline.

## Add these files to the existing repository
Copy the seven `.sv` files into your repository's `rtl/` directory:
- `if_id_register.sv`
- `id_ex_register.sv`
- `ex_mem_register.sv`
- `mem_wb_register.sv`
- `forwarding_unit.sv`
- `hazard_detection_unit.sv`
- `branch_control.sv`

## Notes
- The forwarding unit uses `00` = no forwarding, `10` = EX/MEM, `01` = MEM/WB.
- The hazard unit detects a classic load-use hazard. The decode logic must correctly identify whether the instruction uses `rs2`.
- The branch module supports BEQ, BNE, JAL, and JALR decision/target calculation; the main decoder must produce those control signals.
- `id_ex_register` and `ex_mem_register` include flush inputs to inject a bubble when required.
- Pipeline control/flush timing depends on where branches are resolved. This starter assumes you will wire and verify that policy in the top-level datapath.
- Test and debug these modules in your simulator before claiming full CPU functionality.
