# PyJobTools

A really quick logger util for times you can't connect a debugger to Python, such as when jobs are submitted to a remote computer for execution.

## Use

### rlog

rlog appends job information to a log file. It appends a header at the start of execution (as soon as rlog.open is called), and then logs info with a time and traceback.

To use flog, import the module, then call flog.open(path_to_log_file). Once the log is opened, you can use the four logging methods:

* rlog.debug(text)
* rlog.log(text)
* rlog.warn(text)
* rlog.error(text)

Each function is identical -- which you use only changes the "level" column in the log message.

The log will automatically flush after each logging method call. You do not need to close the log file after use.

#### Sample Use

    from PyJobTools import rlog
    rlog.open('/tmp/run.log')
    
    rlog.debug('Reticulating Splines')
    
    def doYaThing():
        rlog.error('Could not do thing')
    
    def extrapolate():
        rlog.debug("Extrapolating...")
        doYaThing()
    
    extrapolate()

#### Sample Output

    /*
    New run of x.py
    Started at 2013-10-31 17:29
    time		level	message			[traceback]
    */
    17:29:16	dbg	Reticulating Splines		[]
    17:29:16	dbg	Extrapolating...		[x.py:extrapolate():13]
    17:29:16	err	Could not do thing		[x.py:doYaThing():11 <- x.py:extrapolate():13]