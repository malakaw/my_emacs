[http://www.emacswiki.org/emacs/WindowsAndRegisters](http://www.emacswiki.org/emacs/WindowsAndRegisters)

Registers are referred to by a single character, therefore, you can use register 1, 2, a, b, etc.

C-x r w – stores the current configuration in a register
C-x r j – restores the configuration from a register
Example:

C-x r w 1 – store the current configuration
C-x 2 – split vertically
C-x 3 – split horizontally
C-x r j 1 – restore the stored window configuration
