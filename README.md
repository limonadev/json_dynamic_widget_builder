# json_dynamic_widget_builder

## Table of Contents

* [Live Example](#live-example)
* [Introduction](#introduction)
* [Understanding the Registry](#understanding-the-registry)
* [Built In Widgets](#built-in-widgets)
* [Using Variables](#using-variables)
* [Dynamic Functions](#dynamic-functions)
* [Creating Custom Widgets](#creating-custom-widgets)


## Live Example

* [Web](https://peiffer-innovations.github.io/json_dynamic_widget_builder/web/index.html#/)


## Introduction

This provides a WYSIWYG editor for creating JSON based widgets that can be renderered via the [json_dynamic_widget](https://pub.dev/packages/json_dynamic_widget) package.  The editor supports a tree-based property-by-property editor or a full JSON based editor.  It also provides a renderer that can render the widget as the properties are being set.

On the right, the editor provides a help pane that will show any available documentation for the currently selected item in the left hand tree view.



## Understanding the Registry

The `JsonWidgetRegistry` is the centralized processing warehouse for building and using the JSON Dynamic Widgets.  Widgets must be registered to the registry to be available for building.  The registry also supports providing dynamic variables and dynamic functions to the widgets that it builds.

When a value changes on the registry, it posts a notification to the [valueStream](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonWidgetRegistry/valueStream.html) so any potential processing logic can be executed.  The dynamic widgets that use variable values also listen to this stream so they can update their widget state when a value they use for rendering change.

The registry always has a default instance that will be used when a substitute registry is not given.  Substitute registeries can be created and used to isolate variables and functions within the app as needed.  For instance, you may want a separate registry per page if each page may set dynamic values on the registryo.  This can prevent the values from one page being overwritten by another.



## Built In Widgets

The structure for all the `args` is defined in each widget builder, which are defined below:

Widget Builders | Example Location
----------------|------------------
[align](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAlignBuilder/fromDynamic.html) | [align.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/align.json)
[animated_align](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedAlignBuilder/fromDynamic.html) | [animated_align.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_align.json)
[animated_container](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedContainerBuilder/fromDynamic.html) | [animated_container.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_container.json)
[animated_cross_fade](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedCrossFadeBuilder/fromDynamic.html) | [animated_cross_fade.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_cross_fade.json)
[animated_default_text_style](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedDefaultTextStyleBuilder/fromDynamic.html) | [animated_default_text_style.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_default_text_style.json)
[animated_opacity](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedOpacityBuilder/fromDynamic.html) | [animated_opacity.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_opacity.json)
[animated_padding](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedPaddingBuilder/fromDynamic.html) | [animated_padding.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_padding.json)
[animated_physical_model](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedPhysicalModelBuilder/fromDynamic.html) | [animated_physical_model.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_physical_model.json)
[animated_positioned](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedPositionedBuilder/fromDynamic.html) | [animated_positioned.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_positioned.json)
[animated_positioned_directional](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedPositionedDirectionalBuilder/fromDynamic.html) | [animated_positioned_directional.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_positioned_directional.json)
[animated_size](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedSizeBuilder/fromDynamic.html) | [animated_size.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_size.json)
[animated_switcher](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedSwitcherBuilder/fromDynamic.html) | [animated_switcher.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_switcher.json)
[animated_theme](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAnimatedThemeBuilder/fromDynamic.html) | [animated_theme.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/animated_theme.json)
[app_bar](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAppBaruilder/fromDynamic.html) | [align.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/align.json)
[aspect_ratio](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAspectRatioBuilder/fromDynamic.html) | [aspect_ratio.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/aspect_rato.json)
[asset_image](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonAspectImageBuilder/fromDynamic.html) | [asset_images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/asset_images.json)
[baseline](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonBaselineBuilder/fromDynamic.html) | [baseline.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/baseline.json)
[button_bar](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonButtonBarBuilder/fromDynamic.html) | [card.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/card.json)
[card](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonCardBuilder/fromDynamic.html) | [card.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/card.json)
[center](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonCenterBuilder/fromDynamic.html) | [center.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/center.json)
[checkbox](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonCheckboxBuilder/fromDynamic.html) | [checkbox.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/checkbox.json)
[circular_progress_indicator](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonCircularProgressIndicatatorBuilder/fromDynamic.html) | [circular_progress_indicator.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/circular_progress_indicator.json)
[clip_oval](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonClipOvalBuilder/fromDynamic.html) | [clips.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/clips.json)
[clip_rect](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonClipRectBuilder/fromDynamic.html) | [clips.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/clips.json)
[clip_rrect](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonClipRRectBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[column](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonColumnBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[conditional](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonConditionalBuilder/fromDynamic.html) | [conditional.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/conditional.json)
[container](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonContainerBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[cupertino_switch](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonCupertinoSwitchBuilder/fromDynamic.html) | [cupertino_switch.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/cupertino_switch.json)
[directionality](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonDirectionalityBuilder/fromDynamic.html) | [directionality.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/directionality.json)
[dropdown_button_form_field](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonDropdownButtonFormFieldBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[elevated_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonElevatedButtonBuilder/fromDynamic.html) | [buttons.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/buttons.json)
[expanded](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonExpandedBuilder/fromDynamic.html) | [conditional.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/conditional.json)
[fitted_box](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFittedBoxBuilder/fromDynamic.html) | [fitted_box.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/fitted_box.json)
[flat_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFlatButtonBuilder/fromDynamic.html) | [conditional.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/conditional.json)
[flexible](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFlexibleBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[floating_action_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFloatingActionButtonBuilder/fromDynamic.html) | [buttons.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/buttons.json)
[form](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFormBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[fractional_translation](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFractionalTranslationBuilder/fromDynamic.html) | [fractional_translation.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/fractional_translation.json)
[fractionally_sized](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonFractionallySizedBoxBuilder/fromDynamic.html) | [fractionally_sized.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/fractionally_sized.json)
[gesture_detector](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonGestureDetectorBuilder/fromDynamic.html) | [gestures.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/gestures.json)
[hero](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonHeroBuilder/fromDynamic.html) | [asset_images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/asset_images.json)
[icon](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonIconBuilder/fromDynamic.html) | [card.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/card.json)
[ignore_pointer](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonIgnorePointerBuilder/fromDynamic.html) | [gestures.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/gestures.json)
[indexed_stack](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonIndexedStackBuilder/fromDynamic.html) | [indexed_stack.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/indexed_stack.json)
[ink_well](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonInkWellBuilder/fromDynamic.html) | [asset_images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/asset_images.json)
[input_error](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonInputErrorBuilder/fromDynamic.html) | [input_error.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/input_error.json)
[interactive_viewer](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonInteractiveViewerBuilder/fromDynamic.html) | [interactive_viewer.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/interactive_viewer.json)
[intrinsic_height](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonIntrinsicHeightBuilder/fromDynamic.html) | [intrinsic_height.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/intrinsic_height.json)
[intrinsic_width](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonIntrinsicWidthBuilder/fromDynamic.html) | [intrinsic_width.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/intrinsic_width.json)
[limited_box](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonLimitedBoxBuilder/fromDynamic.html) | [limited_box.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/limited_box.json)
[linear_progress_indicator](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonLinearProgressIndicatorBuilder/fromDynamic.html) | [linear_progress_indicator.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/linear_progress_indicator.json)
[list_tile](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonListTileBuilder/fromDynamic.html) | [card.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/card.json)
[list_view](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonListViewBuilder/fromDynamic.html) | [list_view.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/list_view.json)
[material](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonMaterialBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[memory_image](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonMemoryImageBuilder/fromDynamic.html) | [images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/images.json)
[network_image](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonNetworkImageBuilder/fromDynamic.html) | [images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/images.json)
[offstage](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonOffstageBuilder/fromDynamic.html) | [offstage.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/offstage.json)
[opacity](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonOpacityBuilder/fromDynamic.html) | [opacity.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/opacity.json)
[outlined_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonOutlinedButtonBuilder/fromDynamic.html) | [buttons.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/buttons.json)
[overflow_box](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonOverflowBoxBuilder/fromDynamic.html) | [overflow_box.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/overflow_box.json)
[padding](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonPaddingBuilder/fromDynamic.html) |  [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[placeholder](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonPlaceholderBuilder/fromDynamic.html) | [placeholder.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/placeholder.json)
[popup_menu_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonPopupMenuButtonBuilder/fromDynamic.html) | [popup_menu_button.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/popup_menu_button.json)
[positioned](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonPositionedBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[radio](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonRadioBuilder/fromDynamic.html) | [radio.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/radio.json)
[raised_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonRaisedButtonBuilder/fromDynamic.html) | [raised_button.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/raised_button.json)
[row](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonRowBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[safe_area](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSafeAreaBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[save_context](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSaveContextBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[scaffold](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonScaffoldBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[set_value](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSetValueBuilder/fromDynamic.html) | [asset_images.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/asset_images.json)
[single_child_scroll_view](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSingleChildScrollViewBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[sized_box](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSizedBoxBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[stack](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonStackBuilder/fromDynamic.html) | [align.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/align.json)
[switch](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonSwitchBuilder/fromDynamic.html) | [switch.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/switch.json)
[text](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonTextBuilder/fromDynamic.html) | [bank_example.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/bank_example.json)
[text_button](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonTextButtonBuilder/fromDynamic.html) | [buttons.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/buttons.json)
[text_form_field](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonTextFormFieldBuilder/fromDynamic.html) | [form.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/form.json)
[theme](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonThemeBuilder/fromDynamic.html) | [theme.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/theme.json)
[tween_animation](https://pub.dev/documentation/json_dynamic_widget/latest/json_dynamic_widget/JsonTweenAnimationBuilder/fromDynamic.html) | [tween_animation.json](https://github.com/peiffer-innovations/json_dynamic_widget/blob/main/example/assets/pages/tween_animation.json)


## Using Variables

Variables can be defined on the `JsonWidgetRegistry` that is used to render the dynamic widgets.  Within the JSON, the template engine uses the mustache format for variable references.  Example: `{{variableName}}`.

A variable can be used in any of the `child` / `children` / `args` values and for certain types of properties, a variable reference iw the only way to actually assign that value.

Widgets that accept user input will assign that user input to a variable named the value inside of the `id` option, if an `id` exists.  This allows widgets the ability to listen to input value updates.

The built in variables are defined below:

Variable Name    | Example | Description
-----------------|---------|------------
`*curve_name*_curve` | <ul><li>`{{linear_curve}}`</li><li>`{{bounce_in_curve}}`</li></ul> | Provides a `const` instance of any of the [Curves](https://api.flutter.dev/flutter/animation/Curves-class.html#constants) const values. The name of the Curve constant should be transformed into snake_case.

## Dynamic Functions

Similar to the [variables](#using-variables), the `JsonWidgetRegistry` supports registering dynamic functions that can be called to create values.  If a value is a dynamic function then it must begin and end with two pound signs: `##`.  For example: `##set_value(variableName, 5)##`.  Dynamic values can refer to variables using the mustache format.

The built in functions are defined below:

Function Name    | Example | Args | Description
-----------------|---------|------|------------
`navigate_named` | `##navigate_named(home, {{someValue}})##` | <ol><li>The route name</li><li>Optional: an arguments object to provide</li></ol> | Navigates to the named route.  The `GlobalKey<NavigatorState>` must be provided to the registry before this will work.
`navigate_pop`   | `##navigate_pop(false)##` | <ol><li>Optional: the value to pop with</li></ol> | Pop's the navigator stack.  The `GlobalKey<NavigatorState>` must be provided to the registry before this will work.
`noop`           | `##noop()##` | n/a | Simple no-arg no-op function that can be used to enable buttons for UI testing.
`remove_value`   | `##remove_value(varName)##` | <ol><li>The variable name</li></ol> | Removes the variable named in the first argument from the registry.
`set_value`      | `##set_value(varName, some value)##` | <ol><li>The variable name</li><li>The variable value</li></ol> | Sets the value of the variable in the registry.


## Creating Custom Widgets

Creating a custom widget requires first creating a `JsonWidgetBuilder` for the widget you would like to add.

For example, if you would like to create a new widget that can render a SVG, you would create a `SvgWidgetBuilder` like the following:

```dart
import 'package:child_builder/child_builder.dart';
import 'package:flutter/material.dart';
import 'package:json_class/json_class.dart';
import 'package:json_dynamic_widget/json_dynamic_widget.dart';
import 'package:json_theme/json_theme.dart';
import 'package:meta/meta.dart';
import 'package:websafe_svg/websafe_svg.dart';

class SvgBuilder extends JsonWidgetBuilder {
  SvgBuilder({
    this.asset,
    this.color,
    this.height,
    this.url,
    this.width,
  })  : assert(asset == null || url == null),
        assert(asset != null || url != null);

  static const type = 'svg';

  final String asset;
  final Color color;
  final double height;
  final String url;
  final double width;

  static SvgBuilder fromDynamic(
    dynamic map, {
    JsonWidgetRegistry registry,
  }) {
    SvgBuilder result;

    if (map != null) {
      result = SvgBuilder(
        asset: map['asset'],
        color: ThemeDecoder.decodeColor(
          map['color'],
          validate: false,
        ),
        height: JsonClass.parseDouble(map['height']),
        url: map['url'],
        width: JsonClass.parseDouble(map['width']),
      );
    }

    return result;
  }

  @override
  Widget buildCustom({
    ChildWidgetBuilder childBuilder,
    @required BuildContext context,
    @required JsonWidgetData data,
    Key key,
  }) {
    assert(
      data.children?.isNotEmpty != true,
      '[SvgBuilder] does not support children.',
    );

    return asset != null
        ? WebsafeSvg.asset(
            asset,
            color: color,
            height: height,
            width: width,
          )
        : WebsafeSvg.network(
            url,
            color: color,
            height: height,
            width: width,
          );
  }
}
```

Widget builders can also have well defined JSON schemas associated to them.  If a widget builder has an associated JSON schema then in DEBUG modes, the JSON for the widget will be processed through the schema validator before attempting to build the widget.  This can assist with debugging by catching JSON errors early.

An example schema for the `SvgWidgetBuilder` might look something like this:
```dart
import 'package:json_theme/json_theme_schemas.dart';

class SvgSchema {
  static const id =
      'https://your-url-here.com/schemas/svg';

  static final schema = {
    r'$schema': 'http://json-schema.org/draft-06/schema#',
    r'$id': '$id',
    'title': 'SvgBuilder',
    'type': 'object',
    'additionalProperties': false,
    'properties': {
      'asset': SchemaHelper.stringSchema,
      'color': SchemaHelper.objectSchema(ColorSchema.id),
      'height': SchemaHelper.numberSchema,
      'url': SchemaHelper.stringSchema,
      'width': SchemaHelper.numberSchema,
    },
  };
}
```

Once the builder has been created, it needs to be registered with a `JsonWidgetRegistry`.  This must be done before you ever reference the widget.  It's recommended, but not required, that this registration happen in your app's `main` function.

When registring the widget, you can create a new instance of the registry, or simply get a reference to the default instance, which is the approach below follows.

```dart
  var registry = JsonWidgetRegistry.instance;
  registry.registerCustomBuilder(
    SvgBuilder.type,
    JsonWidgetBuilderContainer(
      builder: SvgBuilder.fromDynamic,
      schemaId: SvgSchema.id, // this is optional
    ),
  );
```

Once the widget is registered, you can safely use the registry to build the widget from JSON.  For this example widget, the following JSON would construct an instance:

```json
{
  "type": "svg",
  "args": {
    "asset": "assets/images/visa.svg",
    "color": "#fff",
    "height": 40,
    "width": 56
  }
}
```
