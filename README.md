The library is very simple to use, you use it basically the same way you would use [Malinskiy's](https://github.com/Malinskiy/SuperRecyclerView){:target="_blank"}, but there are some things you can do the C# way, like event handling.

Here's an example of a simple activity that makes use of the library:

    using Android.App;
    using Android.OS;
    using Android.Support.V7.Widget;
    using Com.Malinskiy.Superrecyclerview;

    namespace Com.Example.Activities
    {
        [Activity(Label = "MainActivity")]
        public class MainActivity : Activity, IOnMoreListener
        {
            SuperRecyclerView ItemsRecyclerView;
            YourOwnAdapter ListAdapter;

            protected override void OnCreate(Bundle savedInstanceState)
            {
                SetContentView(Resource.Layout.UserList);

                ItemsRecyclerView = FindViewById<SuperRecyclerView>(Resource.Id.itemsRecyclerView);

                RecyclerView.LayoutManager layoutManager = new LinearLayoutManager(this);
                ListAdapter = new YourOwnAdapter();

                ItemsRecyclerView.SetLayoutManager(layoutManager);
                
                //Works well one way or the other, pick the one you fancy
                //ItemsRecyclerView.More += ItemsRecyclerView_OnMoreAsked;
                ItemsRecyclerView.SetupMoreListener(this, 10);
                
                ItemsRecyclerView.Adapter = ListAdapter;

                base.OnCreate(savedInstanceState);
            }

            protected override void OnDestroy()
            {
                base.OnDestroy();

                //Always a good practice to do this :D
                ItemsRecyclerView.More -= ItemsRecyclerView_OnMoreAsked;
            }

            void ItemsRecyclerView_OnMoreAsked(object sender, MoreEventArgs args)
            {
                //Your logic of adding items to the RecyclerView goes here.
                //You can access the parameters typically passed to OnMoreAsked as properties of the "args" object. 
            }

            public void OnMoreAsked(int overallItemsCount, int itemsBeforeMore, int maxLastVisiblePosition)
            {
                //You can still implement OnMoreAsked() the Java way ;)
            }
        }
    }



Also available as a NuGet Package:

https://www.nuget.org/packages/Tharkius.SuperSharpRecyclerView/1.0.0
