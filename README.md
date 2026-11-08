# NSX-1 Scene Recall

SIMPL+ module for Crestron control processors that recalls a scene of an NSX-1 lighting group over RS485.

When one of the digital inputs `Scene[1]` to `Scene[8]` is pressed, the module builds the 12-character command
`g<group 3 digits>sccc<scene 4 digits>` and sends it to `TX$`. Connect `TX$` to the `TX$` of the COM port
that is wired to the NSX-1 line.

| Item | Value |
|---|---|
| Inputs | `Scene[1]` to `Scene[8]` (digital). `Scene[1]` = scene 0 ... `Scene[8]` = scene 7 |
| Outputs | `TX$` (serial): the command. `Log$` (serial, optional): `<Reference Name>: <command>` for SIMPL Debugger |
| Parameter | `Group_Number` (1 to 999, no default value) |
| Command | `g%03dsccc%04d`, for example `g010sccc0001` (group 010, scene 1). No CR/LF |
| COM port | RS485, 9600 bps, 8 data bits, no parity, 1 stop bit |
| Targets | 3-Series and 4-Series |

## Files

| File | Content |
|---|---|
| `NSX-1 Scene Recall.usp` | SIMPL+ source (CRLF line endings) |
| `NSX-1 Scene Recall.pdf` | Help: symbol, command format, use in SIMPL Windows, Reference Name, notes |

## Use

1. Put both files in your user SIMPL+ folder.
2. Open the `.usp` in SIMPL+, select 3-Series and 4-Series in Build > Control System Target, and compile.
3. In SIMPL Windows, place one symbol per group, enter `Group_Number`, connect the buttons to `Scene[n]`
   and `TX$` to the COM port.

Each command is also output to `Log$` as `<Reference Name>: <command>`, for example `Living: g010sccc0001`.
Give `Log$` a signal name to watch it in SIMPL Debugger. Reference Name and `Log$` may be left empty.

The help PDF opens from the symbol in SIMPL Windows (`#HELP_PDF_FILE`).

## Notes

- Keep CRLF line endings in the `.usp` file. A file with LF only fails to compile.
- The lighting modules do not reply to a scene command.
- Messages from the SIMPL+ `Trace` function did not appear in SIMPL Debugger or the Text Console in a test on site,
  so the module uses the `Log$` output instead.

## License

MIT License. Free to use, modify and redistribute, including for commercial use. See [LICENSE](LICENSE).

SAIence — https://saience.jp/
