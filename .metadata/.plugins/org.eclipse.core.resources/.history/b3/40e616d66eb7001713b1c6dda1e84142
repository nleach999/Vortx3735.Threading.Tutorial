import edu.wpi.first.wpilibj.networktables.NetworkTable;
import edu.wpi.first.wpilibj.tables.ITable;
import edu.wpi.first.wpilibj.tables.ITableListener;


/*
 * Nathan Leach (October 2017)
 * 
 * This is a simple concurrency/multi-threading example.
 * 
 * Run OutlineViewer in server mode on your machine before starting this program:
 * 
 * java -jar OutlineViewer.jar
 * 
 *
 * This connects to the NetworkTables server (OutlineViewer in this case) and registers a
 * boolean variable "ResetCounter" with the default value of false.  The program then
 * prints out an incrementing number in the console.  If the value of ResetCounter is
 * set to "true" in the OutlineViewer, the program should immediately start counting
 * starting from 0 again amd the value in the OutlineViewer should be reset back to false.
 * 
 * The program will appear to not set the counter back to 0 yet will set the value of
 * ResetCounter to false immediately after being set to true.
 * 
 * Then, if you uncomment the block of commented code in the countAndPrint method, it appears
 * to work fine.  Why?
 * 
 * 
 */
public class Concur implements ITableListener {

	private int _counter;

	private Concur() {
		// Connect to local NetworkTables server
		NetworkTable.setClientMode();
		NetworkTable.setIPAddress("localhost");
		NetworkTable.initialize();

		
		// Initialize the reset counter value we'll read.
		NetworkTable t = NetworkTable.getTable("");
		t.putBoolean("ResetCounter", false);
		
		t.addTableListener(this, true);
		
	}

	private void countAndPrint() {
		while (true) {

			int next = _counter + 1;
			System.out.println("Counter: " + _counter);
			_counter = next;

			
// Uncomment this block of code to get it to work.
//			try {
//				Thread.sleep(1);
//			} catch (InterruptedException e) {
//				break;
//			}
			
		}
	}


	@Override
	public void valueChanged(ITable table, String key, Object value, boolean isNew) {
		System.out.println(String.format("valueChanged: Key: {%s} Value: {%s} isNew: {%s}", key, value, isNew));
		
		Boolean reset = (Boolean) value;
		
		if (key.compareTo("ResetCounter") == 0 && reset)
		{
			_counter = 0;
			table.putBoolean(key, false);
		}
		
	}

	public static void main(String args[]) {
		Concur instance = new Concur();
		instance.countAndPrint();
	}
}
