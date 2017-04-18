<!---
    Open Security Analysis Workbench (OpenSAW) - A concolic security test tool
    Copyright (C) 2016 Ericsson AB

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; version 2 of the License.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
--->
    #Currently the only concolic engine is PinBap, if you follow the instructions here you should be able to create
    # a drop in replacement for this concolic engine and modify the few references to PinBap in the pin.py and bap.py
    # to references to your ConcolicEngine object.
    
    #Note, the pin.py and bap.py can run on any ConcolicEngine and not only the PinBap engine!
    # Please be aware that this documentation may not be fully up to date, please verify with
    # PinBap.py 
    
    # Class name of your trace-handling class. Each instance
    # should take a input and a trace and be able to produce 
    # new inputs and give information about the trace. 
    class ConcolicEngine(object):
        # Load a trace file and prepare to modify branches
        def __init__(self, trace_file, input_file):
            
        # Remove trace and temporary files created for trace
        def cleanup(self):
        
        # Return a error message describing why isSuccess is False
        def getDebugString(self):
    
        # Return absolute path to the input file that created this trace
        def getInputFile(self):
    
        # Return True the trace linked to this object was successfully created
        def isSuccess(self):
    
        # Returns the absolute path to the trace
        def getFilename(self):
    
        # Remove this trace and related temporary files except the input file
        # that generated the trace
        def remove(self):
    
        # Removes files that are used for coverage reporting of this trace.
        def removeCoverage(self):
    
        # Returns what signal killed the application being traced. Return None if no signal
        def getSignal(self):

        # Return a dictionary of block_id -> taken_branches_id
        # where taken_branches_id is an integer combination of the flags:
        # 0 - Non conditional branch
        # 1 - Left branch taken
        # 2 - Right branch taken
        # 4 - Conditional branch
        def getCoverage(self):
        
        # Return a list of ids representing executed blocks in the order they were executed.
        def getBblHashes(self):
        
        # Returns a list of integers representing the number of instructions in the block from getBblHashes() with the same index
        def getInsCounts(self):
        
        # returns tuple (new_input, has_changed)
        # new_input is a binary string representing input required to take other path at branch[branch_number]
        # has_changed is true if the new_input is different than the original input that generated this trace.
        def swapBranch(self, branch_number, options):
    
        # Should return a generator of tuples (new_input, has_changed) where the new_input
        # tries to make an unsafe stack write after branch branch_number.
        # A negative branch_number may be received. -1 indicating the last branch.
        def findUnsafeStackWrite(self, branch_number, options):
    
        # Args:
        # input_file: absolute path to an input file
        # logfile: suggested destination path for logfile
        # path: the absolute path to the working directory
        # options: OpenSAW options
        # statistics: OpenSAW statistics object, used to log execution times of sub-tools
        # Return: 
        #    On success: ConcolicEngine object that is linked to the trace generated by running on input from input_file
        #    On error: ConcolicEngine object that returns false on isSuccess(), and a error on getDebugString()
            
        @staticmethod
        def executeTracer(input_file, logfile, path, options, statistics):
        
        # Should be included in the concolic __init__ file, 
        # will be called with an object of statistics/performance.
        # This object should be used to run programs.
        @staticmethod
        def setPerformanceMeasurer(p):