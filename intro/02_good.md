!SLIDE huge
# The Good

!SLIDE
# Objective-C vs Ruby

!SLIDE code fullscreentext

# Objective C

    @@@ c
    @implementation AppDelegate

    @synthesize window = _window;
    @synthesize viewController = _viewController;

    - (BOOL)application:(UIApplication *)application 
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
        self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
        self.viewController = [[ViewController alloc] initWithNibName:@"ViewController" 
                                                               bundle:nil];
        self.window.rootViewController = self.viewController;
        [self.window makeKeyAndVisible];
        return YES;
    }
    @end

!SLIDE code fullscreentext

# Ruby
    
    @@@ ruby
    class AppDelegate
      def application(application, 
          didFinishLaunchingWithOptions:launchOptions)
        @window = UIWindow.alloc.initWithFrame(UIScreen.mainScreen.applicationFrame)
        @window.rootViewController = ViewController.alloc.initWithStyle(UITableViewStylePlain)
        @window.rootViewController.wantsFullScreenLayout = true
        @window.makeKeyAndVisible
        return true
      end
    end

!SLIDE
# No Headers

!SLIDE code fullscreentext
# AppDelegate.h
    @@@ c
    #import <UIKit/UIKit.h>
    
    @class ViewController;
    @interface AppDelegate : UIResponder <UIApplicationDelegate>
    
    @property (strong, nonatomic) UIWindow *window;
    @property (strong, nonatomic) ViewController *viewController;
    @end

!SLIDE
# Less boilerplate

!SLIDE code fullscreentext

    @@@ c
    @class ViewController;
    @interface AppDelegate : UIResponder <UIApplicationDelegate>
    @property (strong, nonatomic) UIWindow *window;
    @property (strong, nonatomic) ViewController *viewController;
    @end
    
    @implementation AppDelegate
    @synthesize window = _window;
    @synthesize viewController = _viewController;
    @end
    
!SLIDE
# Similar

!SLIDE code fullscreentext

# Objective C

    @@@ c
    [delegate application:app didFinishLaunchingWithOptions:options]

# Ruby
    
    @@@ ruby
    delegate.application(app, didFinishLaunchingWithOptions:options)

!SLIDE
# After one week

!SLIDE
# Two type of opinions

!SLIDE huge
# 1. Won't help

!SLIDE
## _"You should just learn Objective-C<br/> and CocoaTouch."_

!SLIDE

## RubyMotion will not simplify your CocoaTouch code (yet)


!SLIDE code fullscreentext

# Ruby
    
    @@@ ruby
    class AppDelegate
      def application(application, 
          didFinishLaunchingWithOptions:launchOptions)
        @window = UIWindow.alloc.initWithFrame(UIScreen.mainScreen.applicationFrame)
        @window.rootViewController = ViewController.alloc.initWithStyle(UITableViewStylePlain)
        @window.rootViewController.wantsFullScreenLayout = true
        @window.makeKeyAndVisible
        return true
      end
    end
    
!SLIDE

## You need to know CocoaTouch!

!SLIDE

## Even you know CocoaTouch... 

!SLIDE
## ... you'll have a hard time typing.


!SLIDE code fullscreentext

# Ruby
    
    @@@ ruby
    delegate.application(app, didFinishLaunchingWithOptions:options)

!SLIDE

# So, Why Border?

!SLIDE huge
# 2. Awesome!

!SLIDE
## _"it will be the creation of the next Rails-for-iOS framework." <br>Dr. Nic_

!SLIDE 
# Wrappers

!SLIDE code fullscreentext

# Objective-C Style Ruby
    
    @@@ ruby
    def showSelection
      UIView.beginAnimations(nil, context:nil)
      UIView.animationDuration = 0.2
      @selection.alpha = 1
      @picker.alpha = 0
      UIView.commitAnimations
    end

!SLIDE

# Ruby Magic

!SLIDE code fullscreentext

    @@@ ruby
    class UIView
      def self.animate_with_block(duration = 0.5)
        beginAnimations(nil, context:nil)
        animationDuration = duration
        yield
        commitAnimations
      end
    end

!SLIDE code fullscreentext
# Objective-C Style Ruby
    
    @@@ ruby
    #Before
    def showSelection
      UIView.beginAnimations(nil, context:nil)
      UIView.animationDuration = 0.2
      @selection.alpha = 1
      @picker.alpha = 0
      UIView.commitAnimations
    end

    # After
    def showSelection
      UIView.animate_with_block(0.2) do
        @selection.alpha = 1
        @picker.alpha = 0
      end
    end
    
!SLIDE huge
# BubbleWrap

!SLIDE
# Simpler HTTP

!SLIDE code fullscreentext

    @@@ ruby
    BubbleWrap::HTTP.get("https://api.github.com/users/matz") do |res|
      p res.body.to_s
    end

!SLIDE 

# Gesture

!SLIDE code fullscreentext

    @@@ ruby
    view.whenTapped do
      UIView.animate_with_block(0.2) do
        @selection.alpha = 1
        @picker.alpha = 0
      end
    end

!SLIDE huge

# Commotion

!SLIDE code fullscreentext

    @@@ ruby
    class Movie < Entity
      field :title, type: String
      field :total_gross, type: Float
      field :createdAt, type: Time
    end

    Movie.create do |movie|
      movie.title = "Iron Man"
      movie.total_gross = 100000000
    end
    
    puts Movie.all
    puts Movie.find_by_title("Iron Man")

