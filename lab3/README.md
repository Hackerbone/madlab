# Crazy lab - learnt to create new pages

```kotlin
class NewsFragment : Fragment(R.layout.fragment_top_news) {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        // Get the text argument passed to the fragment
        val text = arguments?.getString("TAB_TEXT")

        // Set the text in the TextView
        val textView: TextView = view.findViewById(R.id.topNewsText)
        textView.text = text

        // Set up ListView with dynamic data
        val listView: ListView = view.findViewById(R.id.mylist)

        // Sample data - a list of maps with titles and subtitles
        val data = listOf(
            mapOf("title" to "New news channel NIKSBBC found", "subtitle" to "Did not find anything remotely relevant"),
            mapOf("title" to "Tech company announces new product", "subtitle" to "Exciting new tech coming soon"),
            mapOf("title" to "Entertainment industry rocked by new scandal", "subtitle" to "More details to follow"),
            mapOf("title" to "Sports team wins championship", "subtitle" to "Victory after a long season")
        )

        // Define the keys for the data that we want to display in the ListView
        val from = arrayOf("title", "subtitle")
        val to = intArrayOf(R.id.titleTextView, R.id.subtitleTextView)

        // Create the adapter with the data and layout
        val adapter = SimpleAdapter(
            requireContext(),
            data,
            R.layout.list_item_layout, // layout for each row in the ListView
            from,
            to
        )

        // Set the adapter to the ListView
        listView.adapter = adapter
    }

    companion object {
        // Factory method to create a new instance of the fragment with arguments
        fun newInstance(tabText: String): NewsFragment {
            val fragment = NewsFragment()
            val bundle = Bundle()
            bundle.putString("TAB_TEXT", tabText)  // Pass the tab-specific text
            fragment.arguments = bundle
            return fragment
        }
    }
}

```



### View Page Adapter

```kotlin
class ViewPagerAdapter(fragmentActivity: FragmentActivity) : FragmentStateAdapter(fragmentActivity) {

    override fun getItemCount(): Int = 3  // Number of tabs

    override fun createFragment(position: Int): Fragment {
        return when (position) {
            0 -> NewsFragment.newInstance("Top News")  // Fragment for Top News
            1 -> NewsFragment.newInstance("Sports")   // Fragment for Sports
            2 -> NewsFragment.newInstance("Entertainment")  // Fragment for Entertainment
            else -> NewsFragment.newInstance("LOL")  // Fragment for LOL
        }
    }
}
```
