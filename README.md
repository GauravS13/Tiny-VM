# 🚀 Tiny Virtual Machine - 8-bit CPU Emulator

A **single HTML file** containing a complete 8-bit CPU emulator and assembler that runs entirely in your web browser. Built for educational purposes, legacy browser compatibility, and minimal resource usage.

## ✨ **Features**

### **🎯 Core Emulator**
- **8-bit CPU Architecture** with realistic register simulation
- **64KB Memory Space** with memory-mapped I/O
- **17 Instruction Set** covering basic operations
- **Real-time Execution** with step-by-step debugging
- **Memory Protection** preventing system crashes
- **Stack Operations** with overflow protection

### **🔧 Assembler**
- **Two-pass Assembly** with label resolution
- **Code Validation** preventing invalid instructions
- **Error Reporting** with line numbers and descriptions
- **Warning System** for potential issues

### **🎨 Graphics System**
- **64x32 Pixel Display** (256x128 canvas)
- **Memory-mapped Graphics** at address 0x8000-0x8FFF
- **Real-time Updates** when graphics memory changes
- **Color Support** using 8-bit grayscale values

### **📱 User Interface**
- **Split-panel Design** (Editor + Emulator)
- **Real-time Register Display** showing all CPU state
- **Memory Hex Dump** with ASCII representation
- **Performance Monitoring** with cycle counting
- **Responsive Design** for different screen sizes

## 🏗️ **Architecture**

### **CPU Registers**
| Register | Purpose | Size |
|----------|---------|------|
| A | Accumulator | 8-bit |
| B | General Purpose | 8-bit |
| C | General Purpose | 8-bit |
| D | General Purpose | 8-bit |
| PC | Program Counter | 16-bit |
| SP | Stack Pointer | 16-bit |
| FLAGS | Status Flags | 8-bit |

### **Memory Layout**
| Address Range | Purpose | Access |
|---------------|---------|---------|
| 0x0000-0x7FFF | Program Memory | Read/Write |
| 0x8000-0x8FFF | Graphics Memory | Read/Write |
| 0x9000-0xEFFF | System Memory | Read-Only |
| 0xF000-0xFFFF | Stack Memory | Read/Write |

### **Instruction Set**
| Instruction | Opcode | Description | Operands |
|-------------|--------|-------------|----------|
| NOP | 0x00 | No Operation | None |
| HLT | 0x01 | Halt Execution | None |
| MOV | 0x02 | Move Data | Register, Value |
| ADD | 0x03 | Add Registers | Dest, Source |
| SUB | 0x04 | Subtract Registers | Dest, Source |
| CMP | 0x05 | Compare Registers | Reg1, Reg2 |
| JMP | 0x06 | Jump to Address | Address |
| JZ | 0x07 | Jump if Zero | Address |
| JNZ | 0x08 | Jump if Not Zero | Address |
| LOAD | 0x09 | Load from Memory | Register, Address |
| STORE | 0x0A | Store to Memory | Register, Address |
| PUSH | 0x0B | Push to Stack | Register |
| POP | 0x0C | Pop from Stack | Register |
| CALL | 0x0D | Call Subroutine | Address |
| RET | 0x0E | Return from Subroutine | None |
| INC | 0x0F | Increment Register | Register |
| DEC | 0x10 | Decrement Register | Register |

## ✅ **What Works**

### **Supported Features**
- ✅ **Basic Arithmetic**: Addition, subtraction, increment, decrement
- ✅ **Data Movement**: Register-to-register and immediate values
- ✅ **Control Flow**: Jumps, conditional jumps, subroutines
- ✅ **Memory Operations**: Load, store with bounds checking
- ✅ **Stack Operations**: Push, pop with overflow protection
- ✅ **Labels**: Basic label support for jumps and calls (e.g., `COUNT:`, `DRAW:`)
- ✅ **Comments**: Assembly-style comments with semicolon
- ✅ **Hex Numbers**: 0x prefix for hexadecimal values
- ✅ **Graphics**: Memory-mapped display with real-time updates

**Note**: Labels are NOT instructions - they're markers for addresses. Use descriptive names like `COUNT:`, `DRAW:`, `DONE:`.

### **Example Programs**
```assembly
; Simple Counter (0 to 10)
MOV A, 0
COUNT: INC A
CMP A, 10
JNZ COUNT
HLT

; Add Two Numbers
MOV A, 42
MOV B, 10
ADD A, B
HLT

; Graphics Demo (draw white pixels)
MOV A, 0x80        ; Graphics memory start (0x8000)
MOV B, 0x00        ; Counter
MOV C, 0xFF        ; White color (255)
DRAW: STORE C, A   ; Draw pixel at address A
INC A              ; Next memory address
INC B              ; Increment counter
CMP B, 10          ; Compare with limit
JNZ DRAW           ; Continue if not done
HLT                ; Stop execution
```

## ❌ **What Doesn't Work**

### **Unsupported Features**
- ❌ **Floating Point**: No decimal numbers (only integers 0-255)
- ❌ **Strings**: No text literals or string operations
- ❌ **Arrays**: No array indexing or complex data structures
- ❌ **Indirect Addressing**: No [register] syntax
- ❌ **Large Values**: No numbers > 255 (8-bit limit)
- ❌ **System Memory Writes**: Cannot write to 0x9000+
- ❌ **External I/O**: No file operations or network access
- ❌ **Interrupts**: No interrupt handling system

### **Limitations**
- **Memory**: Limited to 64KB total address space
- **Performance**: Single-threaded execution
- **Precision**: 8-bit arithmetic only
- **Browser**: Requires JavaScript-enabled browser

## 🚀 **How to Run**

### **Method 1: Direct File Opening**
1. **Download** the `tiny-vm.html` file
2. **Double-click** the file to open in your default browser
3. **Or** drag and drop into any modern web browser

### **Method 2: Web Server (Recommended)**
1. **Start a local web server**:
   ```bash
   # Python 3
   python -m http.server 8000
   
   # Python 2
   python -m SimpleHTTPServer 8000
   
   # Node.js
   npx http-server
   
   # PHP
   php -S localhost:8000
   ```
2. **Open** `http://localhost:8000/tiny-vm.html` in your browser

### **Method 3: Online Hosting**
1. **Upload** to any web hosting service (GitHub Pages, Netlify, etc.)
2. **Access** via the provided URL

## 📖 **Usage Instructions**

### **1. Writing Assembly Code**
- **Use the text editor** on the left panel
- **Follow the syntax**: `INSTRUCTION operand1, operand2`
- **Add labels** with `LABEL:` syntax (e.g., `START:`, `LOOP1:`, `DONE:`)
- **Include comments** with semicolon `;`

**Important**: Labels are NOT instructions! They're markers that get converted to addresses.
- ✅ **Correct**: `COUNT: MOV A, 42` (label followed by instruction)
- ✅ **Correct**: `DRAW: INC A` (descriptive label name)
- ❌ **Wrong**: Treating labels as instructions

### **2. Assembling Code**
1. **Click "Assemble"** to convert assembly to machine code
2. **Check for errors** in the status bar
3. **Resolve any validation errors** before proceeding

### **3. Running Programs**
- **Click "Run"** to execute continuously
- **Click "Step"** to execute one instruction at a time
- **Click "Reset"** to restart the program
- **Click "Clear"** to clear the editor

### **4. Using Help & Samples**
- **Click "Help"** to see the complete assembly guide
- **Click "Samples"** to load working example programs
- **Choose a sample** by entering its number

### **5. Monitoring Execution**
- **Watch registers** update in real-time
- **Monitor memory** in the hex dump view
- **Check graphics** on the canvas display
- **Read status** in the bottom status bar

## 🔧 **Troubleshooting**

### **Common Issues**

#### **"Help/Samples buttons not working"**
- **Solution**: Refresh the page and try again
- **Cause**: JavaScript initialization issue

#### **"Program runs forever"**
- **Solution**: Check for missing HLT instruction
- **Cause**: Infinite loop without halt

#### **"Memory not updating"**
- **Solution**: Ensure program assembled successfully
- **Cause**: Assembly errors or memory not loaded

#### **"Graphics not showing"**
- **Solution**: Write to addresses 0x8000-0x8FFF with non-zero values
- **Cause**: Writing to wrong memory region or using zero values (black pixels)

#### **"Graphics memory always black"**
- **Solution**: Use values 0x01-0xFF for visible pixels (0x00 = black, 0xFF = white)
- **Solution**: Try Sample #6 (Simple Graphics) for working example
- **Cause**: Default memory is zero (black pixels) or writing zero values

#### **"Browser compatibility issues"**
- **Solution**: Use modern browser (Chrome, Firefox, Safari, Edge)
- **Cause**: Legacy browser limitations

### **Debug Tips**
1. **Use Step mode** to see instruction-by-instruction execution
2. **Check console** for detailed error messages
3. **Monitor registers** to understand program flow
4. **Use small test programs** before complex code
5. **Verify memory addresses** are within valid ranges

## 🌐 **Browser Compatibility**

### **Fully Supported**
- ✅ Chrome 60+
- ✅ Firefox 55+
- ✅ Safari 12+
- ✅ Edge 79+

### **Partially Supported**
- ⚠️ Internet Explorer 11 (ES5 compatibility)
- ⚠️ Older mobile browsers

### **Not Supported**
- ❌ Internet Explorer 10 and below
- ❌ Very old mobile browsers

## 📊 **Performance**

### **Resource Usage**
- **Memory**: < 10MB RAM usage
- **CPU**: Minimal overhead
- **Storage**: Single HTML file (~50KB)
- **Network**: No external dependencies

### **Execution Speed**
- **Default**: 10 instructions per second
- **Maximum**: Limited by browser performance
- **Real-time**: Immediate register updates
- **Graphics**: 60 FPS canvas updates

## 🎓 **Educational Value**

### **Learning Objectives**
- **CPU Architecture**: Understanding registers and memory
- **Assembly Language**: Basic instruction syntax
- **Memory Management**: Address spaces and protection
- **Graphics Programming**: Memory-mapped displays
- **Debugging**: Step-by-step program execution

### **Target Audience**
- **Computer Science Students**: CPU architecture concepts
- **Programming Beginners**: Assembly language introduction
- **Hobbyists**: Simple computer simulation
- **Educators**: Interactive teaching tool

## 🔮 **Future Enhancements**

### **Planned Features**
- **More Instructions**: Multiplication, division, bit operations
- **Sound Support**: Audio output via Web Audio API
- **Save/Load**: Program persistence
- **Breakpoints**: Advanced debugging features
- **Performance Profiling**: Detailed execution analysis

### **Possible Extensions**
- **Network Support**: Multi-player emulation
- **Plugin System**: Custom instruction sets
- **3D Graphics**: WebGL integration
- **File System**: Basic file I/O simulation

## 📄 **License**

This project is open source and available under the MIT License. Feel free to use, modify, and distribute as needed.

## 🤝 **Contributing**

Contributions are welcome! Areas for improvement:
- **Bug fixes** and error handling
- **Performance optimizations**
- **Additional instructions**
- **UI/UX improvements**
- **Documentation updates**

## 📞 **Support**

### **Getting Help**
1. **Check this README** for common solutions
2. **Review the Help button** in the emulator
3. **Try sample programs** to verify functionality
4. **Check browser console** for error messages

### **Reporting Issues**
When reporting problems, include:
- **Browser version** and operating system
- **Steps to reproduce** the issue
- **Expected vs actual behavior**
- **Console error messages** (if any)

---

**Happy Programming! 🎉**

*The Tiny VM - Making CPU architecture accessible to everyone.*
